# Finance 수집 파이프라인 재설계: raw 직접 기록 → inbox 큐잉 + Claude Code 요약

**작성일**: 2026-08-01
**작성자**: Claude Code
**목적**: `docs/260801_01_current-system-architecture.md` §5에서 발견한 크론
무결성 이슈(로컬 모델이 `file-article.py` 호출을 건너뛰고 `write_file`로
직접 raw 레코드를 작성해 frontmatter/sha256/log.md가 누락된 문제)를 구조적으로
재발 불가능하게 만들고, 사용자 제안대로 "cron은 제목/URL만 큐잉 → 이후
Claude Code가 각 항목을 직접 요약해 등록"하는 방식으로 파이프라인을 재설계함.

---

## 1. 배경

기존 설계(`docs/260731_05`)는 크론 실행 중 로컬 12B 모델(gemma4:12b)이
`file-article.py`를 호출하도록 프롬프트로 지시하는 방식이었다. 이번 세션에서
실제 야간 실행 로그를 대조해보니, `execute_code`가 크론 환경에서 BLOCKED되자
모델이 스크립트 호출을 우회하고 `write_file`로 직접 raw 파일을 작성해버린
사례가 확인됐다 (`docs/260801_01` §5). 문제의 근본 원인은 "로컬 모델이
반드시 결정론적 스크립트를 호출한다"는 가정 자체가 강제되지 않는다는
것이었다.

사용자 제안: 크론은 제목/URL(및 최소한의 메타데이터)만 한 곳에 적어두고,
실제 요약은 특정 시점에 Claude Code가 각 항목을 읽고 직접 작성하는 방식으로
바꾸자는 것. 이 구조는 `SCHEMA.md`의 "raw는 최초 캡처 후 불변" 원칙과도
더 잘 맞는다 — 미완성 초안이 raw로 들어가는 대신, 완성된 것만 raw로 간다.

## 2. 변경 사항

### 2.1 `~/.hermes/scripts/finance-morning-digest.py` 전면 재작성

- **이전**: RSS 수집 → 기사별 body 파일 선기록 → JSON을 에이전트 프롬프트에
  주입 → 에이전트가 태그/검증판정을 정하고 `file-article.py`를 호출해 raw에
  직접 등록.
- **이후**: RSS 수집 → `raw/articles/` + `inbox/`의 기존 `source`와 대조해
  중복 제거(24h 컷오프) → 신규 기사마다 `inbox/finance-<slug>.md`를
  **스크립트가 직접, 결정론적으로** 작성(제목/URL/게재일/저자/캡처시각/
  RSS teaser + 승격 명령 스니펫) → 신규 건이 있으면 제목·링크 목록을,
  없으면 빈 문자열을 stdout으로 출력.
- LLM 판단(태그 선택, 검증 여부, frontmatter 작성)이 이 단계에서 완전히
  사라짐 — canonical/raw에 아무것도 쓰지 않으므로 오염 리스크가 없다.

### 2.2 Hermes cron job을 `--no-agent`로 전환

```
hermes cron edit f7215c8998ff --no-agent --prompt ""
```

- **이전**: `Mode: agent`(gemma4:12b가 매 실행마다 판단·도구 호출).
- **이후**: `Mode: no-agent (script stdout delivered directly)` — 스크립트
  자체가 job이며, LLM 호출이 전혀 일어나지 않는다. stdout이 비어 있으면
  무음 배달(디스코드 메시지 없음).
- 스케줄(`0 3 * * *`), 배달 대상(`discord:1532595343110307900`), workdir는
  변경하지 않음.
- `hermes cron run f7215c8998ff`로 실행 검증: 신규 후보가 이미 큐에 있어
  0건 발견 → 로그에 `empty stdout — silent run` 확인, LLM API 호출 없음
  (에이전트 로그에 API call 기록 자체가 없음).

### 2.3 `raw/articles/` 무결성 이슈 2건 해소

`docs/260801_01`에서 발견한 frontmatter 없는 raw 레코드 2건을 이번 재설계
검증을 겸해 정리함:

1. 각 기사 원문을 `curl`로 재수신.
   - Dow/S&P/Nasdaq 기사는 JSON-LD `articleBody`에서 실제 본문(1,876자)을
     확보해 직접 5문장 요약을 작성.
   - Apple 기사는 원문 본문 접근이 안 되어(og:description 티저만 존재)
     티저 기반으로 작성하되, 위 Dow 기사 본문에 있는 "Apple -7%,
     Services/China 부진" 서술과 대조해 핵심 주장을 교차검증함.
2. `file-article.py`로 두 건을 재등록(frontmatter/sha256/log.md 전부
   스크립트가 결정론적으로 처리) — 기존 malformed 파일은 삭제.
3. `log.md`에 `ingest` 2건 + 이번 조치를 요약한 `repair` 1건 추가.

## 3. 새 데이터 플로우 (요약)

```
Yahoo Finance RSS
  → finance-morning-digest.py (--no-agent, 순수 스크립트, LLM 없음)
      · 중복 제거 (raw/articles + inbox 기존 source 대조)
      · inbox/finance-<slug>.md 결정론적 생성 (제목/URL/teaser만)
  → (사람 또는 다음 Claude Code 세션이 임의 시점에 처리)
Claude Code 세션
  → inbox/finance-*.md 하나씩 읽음
  → 원문 fetch (curl/WebFetch) + 실제 요약 직접 작성
  → file-article.py 호출 (frontmatter·sha256·log.md 결정론 처리)
  → raw/articles/*.md 완성, inbox 항목 삭제
  → (2개 이상 소스 누적 시) canonical 승격 검토는 여전히 사람의 몫
```

## 4. 현재 남은 큐

이번 검증 과정에서 스크립트를 실제로 1회 실행해 `inbox/`에 신규 기사 9건이
정상적으로 큐잉되어 있다 (모기지/CD 금리, 여행자보험 등 개인재무 뉴스 다수
포함 — Yahoo RSS가 지금 반환한 항목 그대로이며 별도 주제 필터링은 하지
않음). 이번 작업 범위는 파이프라인 재설계였으므로 9건 전체를 raw로
승격하지는 않았다. 다음 Claude Code 세션에서 각 `inbox/finance-*.md`에
적힌 안내 명령을 따라 처리하면 된다.

## 5. 다음 단계 (제안, 미실행)

- `inbox/`에 finance 큐가 쌓였을 때 Claude Code에게 "inbox 처리해줘"라고
  요청하면 일괄 승격하는 루틴을 정례화할지 결정.
- 이전에 수동으로 등록된 `korean-stocks-jump-record-14pct-ai-optimism.md`는
  `tags: news, equity, macro`를 쓰고 있으나 `news`는 `SCHEMA.md` 등록
  태그 목록에 없음 (`file-article.py`라면 이 태그를 ERROR로 거부했을
  것). 이번 작업 범위 밖이라 수정하지 않았으니 별도로 다뤄야 함.
