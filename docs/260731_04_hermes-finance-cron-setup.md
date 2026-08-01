# Hermes 새벽 3시 Yahoo Finance 자동 수집 파이프라인 구축

**작성일**: 2026-07-31
**작성자**: Claude Code
**목적**: Hermes Agent(로컬 Ollama)를 이용해 매일 새벽 3시 Yahoo Finance 뉴스를 수집·
검증·분류하고 Discord로 요약을 전달하는 무인 자동화를 구축

---

## 1. 환경 조사 결과

작업 전 `~/.hermes`를 조사해 다음을 확인함:

- Hermes Agent(Nous Research)가 이미 설치돼 있고, 기본 모델이 **로컬 Ollama
  `gemma4:12b`** (`http://127.0.0.1:11434/v1`)로 설정돼 있어 API 비용 없이 실행 가능.
- `DISCORD_BOT_TOKEN`, `DISCORD_HOME_CHANNEL`이 이미 `.env`에 설정돼 있어 Discord
  연동이 즉시 가능한 상태였음.
- `hermes cron create`라는 네이티브 스케줄러가 있어 자연어 프롬프트 + cron
  표현식으로 무인 작업 등록 가능. `--workdir` 옵션을 주면 해당 디렉토리의
  `AGENTS.md`를 자동으로 컨텍스트에 주입함 — 이 위키의 SCHEMA.md/AGENTS.md 규칙을
  Hermes가 매 실행마다 자동으로 인지하게 됨.
- `skills/social-media/xurl`(X 공식 API), `skills/research/blogwatcher`(RSS
  모니터링) 스킬이 레포에 포함돼 있었으나 `blogwatcher-cli` 바이너리는 미설치 상태.

## 2. 시행착오

1. **blogwatcher-cli 설치 후 Yahoo Finance RSS 등록 실패**: `blogwatcher-cli`를
   `~/.local/bin`에 설치하고 `https://finance.yahoo.com/news/rssindex`를
   등록했으나, 스캔 시 `status 429`로 계속 차단됨. 바이너리에 하드코딩된 Go 기본
   User-Agent를 Yahoo가 차단하는 것으로 확인 (커스텀 UA 설정 옵션 없음). 이전
   `curl -A "Mozilla/5.0 ..."` 테스트는 200이 왔던 것과 대조적. → blogwatcher-cli
   등록을 제거하고, 크론 작업 프롬프트에서 브라우저 User-Agent를 붙인 `curl`로
   직접 RSS를 받도록 변경.
2. **`hermes cron create` positional 인자 순서 문제**: `--name`, `--deliver` 같은
   옵션 플래그 뒤에 prompt를 두면 `unrecognized arguments` 에러 발생. `schedule`과
   `prompt` positional 인자는 반드시 옵션 플래그보다 앞에 와야 함을 시행착오로
   확인 후 순서를 바꿔 해결.
3. **Discord 배달 대상 오해 정정**: 사용자가 "기본 채널(origin)"을 선택했으나,
   `origin`은 "명령을 실행한 채팅창으로 되돌려준다"는 의미라 CLI(터미널)에서
   생성하면 Discord로 가지 않음. 이미 설정된 `DISCORD_HOME_CHANNEL`로 보내려면
   `--deliver discord`가 맞다는 것을 코드(`cron/scheduler.py`)에서 확인하고 정정.

## 3. 최종 구성

- **스케줄**: `0 3 * * *` (매일 새벽 3시, KST)
- **작업 디렉토리**: `/SSD1/sjchoi/2nd-brain-system` (AGENTS.md 자동 주입)
- **배달**: `discord` (사전 설정된 `DISCORD_HOME_CHANNEL`)
- **모델**: 사전 설정된 기본값 사용 → 로컬 `gemma4:12b` (API 비용 없음)
- **Job ID**: `f7215c8998ff` (`finance-morning-digest`)

**작업 프롬프트 요지**:
1. `curl`로 Yahoo Finance RSS(`https://finance.yahoo.com/news/rssindex`, 브라우저
   User-Agent 사용)를 받아 지난 24시간 신규 기사 추출, 기존 `raw/articles/`의
   `source` 필드와 대조해 중복 제거.
2. 각 기사 본문을 다시 `curl`로 받아 핵심 수치/주장이 교차 확인되는지 판단, 안
   되면 "미검증"으로 표시 (이번 세션의 SK Hynix 기사 검증 방식과 동일한 절차).
3. `inbox/` 임시 적재 → 검증/신뢰 가능한 항목만 `raw/articles/`로 분류
   (frontmatter: title/source/author/published/created/description/tags/sha256).
4. `log.md`에 `ingest` 액션 항목 추가.
5. **canonical 페이지(entities/concepts/comparisons/queries)는 절대 자동
   생성하지 않음** — 다중 소스 판단과 wikilink 연결성이 필요한 승격은 사람이
   검토.
6. **git add/commit은 하지 않음** — 변경사항은 워킹트리에만 남기고, 리뷰 후
   수동(또는 다음 Claude Code 세션)으로 커밋.
7. 마지막에 Discord로 ingest 건수, 기사 제목/경로, 미검증·이상치 항목을 요약
   전송. 신규 기사가 없으면 아무것도 만들지 않고 그대로 보고.

## 4. 검증

- `hermes cron status` → 게이트웨이 실행 중 확인 (PID 4183054), 1개 활성 작업.
- `hermes cron list` → `finance-morning-digest` job이 `0 3 * * *`, `Deliver:
  discord`, `Workdir: /SSD1/sjchoi/2nd-brain-system`로 정확히 등록됨 확인.
- 다음 실행: `2026-08-01T03:00:00+09:00`.

## 5. 남은 범위 (의도적으로 보류)

- **X(트위터), Reddit**: 이번 단계에선 제외. X는 `xurl` 스킬로 가능하지만 사용자가
  직접 X 개발자 앱/OAuth 토큰을 발급받아야 하고, Reddit도 별도 앱 등록이 필요함.
- **Canonical 승격 자동화**: 지금은 raw ingest까지만 자동화하고, `entities/`나
  `concepts/` 생성은 사람이 review 후 진행. 반복 소스가 쌓이면 재검토.
- **자동 커밋**: 매일 밤 무인 커밋은 하지 않음 — 오분류 리스크를 줄이기 위해
  리뷰 후 커밋하는 흐름 유지.
