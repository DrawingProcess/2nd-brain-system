# finance-morning-digest 크론 신뢰성 수정

**작성일**: 2026-07-31
**작성자**: Claude Code
**목적**: `finance-morning-digest` (job `f7215c8998ff`) 크론이 "Response remained
truncated after 4 continuation attempts"로 실패한 원인을 규명하고, 반복 테스트를 통해
드러난 추가 실패 양상들을 모두 해결

---

## 1. 최초 실패 원인

`~/.hermes/logs/agent.log` 분석 결과, 크래시는 단순 "출력 길이 초과"가 아니라 연쇄
실패였음:

1. 크론 프롬프트가 로컬 모델(gemma4:12b, Ollama)에게 매번 즉흥적으로 `curl`로 RSS를
   받고 `grep/sed/paste`로 XML을 직접 파싱하도록 시켰는데, `<`/`>` 이스케이프 실패로
   셸 명령이 문법 오류를 반복함.
2. 크론 작업은 사람 승인자가 없어 `execute_code`, `-e`/`-c` 스크립트 실행 플래그가
   전부 BLOCKED 처리됨 — 실패를 만회할 수단이 없었음.
3. 반복된 도구 실패 끝에 모델이 13:00~13:03 사이 계속 빈 응답을 냈고, 4번의
   continuation 시도도 회복하지 못해 RuntimeError로 종료.

## 2. 반복 테스트로 드러난 추가 문제와 조치

셸 파싱을 제거한 뒤에도, 실제 검증 실행마다 새로운 실패 양상이 나타나 순차적으로
해결함:

| 발견된 문제 | 증거 | 조치 |
|---|---|---|
| 모델이 frontmatter/sha256을 손으로 써서 오염 (`source: Yahoo Finance`, `created: 2024-05-21`, sha256 필드명 누락) | 1건 테스트 파일 확인 | `~/.hermes/scripts/file-article.py` 신설 — source/created/sha256/log.md 기록을 전부 코드로 결정론적 처리, 등록 안 된 태그는 ERROR로 거부 |
| Yahoo 기사 페이지가 JS 렌더링 SPA라 `requests`로는 내비게이션 메뉴만 잡히고 실제 본문은 못 가져옴 (RSS `description`도 항상 빈 문자열) | 원본 HTML 확인 | `og:description`/`meta description`/JSON-LD에서 실제 teaser 텍스트와 author를 추출하도록 `finance-morning-digest.py` 수정 |
| 여러 기사를 한 번에 처리할 때 본문이 서로 뒤바뀜 (고정 임시 파일 경로 재사용 추정) | Cramer 파일에 Fed 기사 본문·링크가 들어감, 두 파일 sha256 동일 | `file-article.py`에 URL 불일치 가드 추가 (`--body-file`이 다른 기사 URL을 인용하면 ERROR로 거부) |
| 별도 임시 파일에 본문을 옮겨 적는 단계에서 모델이 매번 성의 없게 처리 (플레이스홀더 문장 → 제목 반복) | 4개 파일 전부 동일 문구 / 제목만 반복 | 본문 작성 자체를 에이전트에서 제거 — `finance-morning-digest.py`가 각 기사의 excerpt를 미리 임시 파일로 써서 경로(`body_file`)를 넘기고, 에이전트는 그 경로를 그대로 전달만 함 |

## 3. 최종 아키텍처

- **`~/.hermes/scripts/finance-morning-digest.py`** (cron `--script`, agent 모드):
  RSS 수집 → `raw/articles/` 기존 source와 대조해 중복 제거 → 기사별 실제 페이지에서
  `og:description`/author 추출 → 기사별 body 파일(`/tmp/finance_digest_bodies/`)을
  미리 작성 → JSON(title/link/published/description/excerpt/author/body_file)을
  에이전트 프롬프트에 주입.
- **에이전트(gemma4:12b)의 역할은 판단으로 축소**: 검증됨/미검증 판단, 태그 선택,
  `file-article.py` 호출, 마지막 Discord 요약(3문장) 작성 — 프론트매터·해시·로그
  기록·본문 캡처는 전부 결정론적 코드가 담당.
- **`~/.hermes/scripts/file-article.py`**: 태그 검증, 오늘 날짜, sha256 계산, YAML
  안전 직렬화, log.md ingest 항목 추가, body-file/link URL 일치성 검사까지 전담.

## 4. 검증

시간 필터를 임시로 넓혀(24h → 31h/34h) 실제 후보 기사가 나오게 만든 뒤 `hermes cron
run f7215c8998ff`로 4차례 반복 테스트. 마지막 실행(기사 5건)에서:

- 5건 모두 정확한 frontmatter(올바른 source URL, 오늘 날짜 created, 실제 sha256,
  등록된 태그, 정확한 author) 생성.
- 5건 모두 본문이 실제 각 기사의 teaser와 정확히 일치, 상호 오염 없음.
- log.md에 5건 모두 올바른 형식으로 기록.
- Discord 응답: 상위 3건은 제목/태그/3문장 요약/링크, 나머지 2건은 개수만 언급 —
  요청한 형식과 일치.
- 테스트로 생성된 모든 파일/log.md 변경/임시 파일은 검증 후 제거, 시간 필터는 24h로
  복원 (`git status` 클린 확인).

## 5. 남은 리스크

- 로컬 12B 모델 특성상, 위 표의 실패 양상들은 "이번에 관측된 것"이지 이론적으로 전부
  차단됐다고 보장할 수는 없음. `file-article.py`의 태그/URL 검증 가드가 있어 오류가
  나면 **조용히 오염되기보다 ERROR로 실패**하도록 설계했으므로, 실패 시 Discord로
  에러가 그대로 전달되어 사람이 알아챌 수 있음.
- Yahoo Finance 기사 원문 자체(본문 전체)는 여전히 가져오지 못함 — `og:description`
  teaser(1~2문장)가 유일한 실제 소스 콘텐츠이므로, "핵심 수치 교차검증"의 깊이는
  teaser 수준으로 제한됨.
- 권장: 당분간 `raw/articles/`에 새로 등록되는 항목을 가끔 사람이 훑어보길 권장
  (canonical 승격은 이미 사람 검토 필수이므로 낮은 리스크이지만, raw 캡처 품질도
  주기적으로 확인하는 편이 안전함).
