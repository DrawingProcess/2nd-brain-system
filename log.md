# Wiki Log

> Chronological record of wiki actions. This file is append-only: add entries at
> the end and never rewrite or remove an earlier entry.
>
> Entry heading format: `## [YYYY-MM-DD] <action> | <subject>`
>
> Allowed actions: `ingest`, `create`, `update`, `query`, `lint`, `archive`,
> `delete`, `map`, and `repair`.
>
> Each entry lists every affected repository-relative path. After 500 entries,
> rotate the completed file to `log-YYYY.md` and begin a new `log.md`; preserve the
> completed file unchanged.

## [2026-07-21] ingest | 2nd-Brain 개인지식 관리 원본 배치

- Selection: `understand-chat` identified the 2nd-Brain PKM core subgraph and its one-hop canonical neighbors; their leading frontmatter referenced 13 unique raw sources.
- Created:
  - `raw/notebooklm/2026-07-16-all-notes.md`
  - `raw/notebooklm/codegraph-github.md`
  - `raw/notebooklm/graphify-github.md`
  - `raw/notebooklm/llm-wiki-skill-github.md`
  - `raw/notebooklm/llm-wiki-zotero-notebooklm-youtube.md`
  - `raw/notebooklm/notebooklm-py-github.md`
  - `raw/notebooklm/understand-anything-github.md`
  - `raw/notebooklm/zotero-mcp-github.md`
  - `raw/web/NomaDamasslides-grab Best harness + editor + linter for generating slides in Claude Code  Codex - Claude Design Open Source Alternative.md`
  - `raw/web/stablyaiorca Orca is the ADE for working with a fleet of parallel agents. Run any coding agent with your own subscription. Available on desktop and mobile..md`
  - `raw/youtube/📺 How To Build LLM Wiki In Obsidian 🧠 A Memory Layer For Any Agentic AI.md`
  - `raw/youtube/📺 LLM Wiki를 업그레이드하는 외부 지식 시스템! 연구자를 위한 최강의 조합 Zotero × Notebook × Obsidian x Claude Code.md`
  - `raw/youtube/📺 Orca Is the Free Cursor Killer Nobody's Talking About!.md`
- Updated: `SCHEMA.md`, `AGENTS.md` to register importer-preserved raw directories and legacy hash-coverage handling.
- Integrity: all 13 target files are byte-identical to the source vault; all 8 recorded post-frontmatter body hashes match; 5 legacy web/video captures have no recorded `sha256` and retain their original missing final LF as explicit coverage and format gaps.
- Canonical state: unchanged at 0 pages; `index.md` was not modified.

## [2026-07-21] lint | 0 issues found

- Raw files in the imported source set: 13.
- Source/target byte-identical files: 13.
- Recorded post-frontmatter body hashes checked and matched: 8.
- Documented legacy hash-coverage and final-LF format gaps: 5.
- Invalid UTF-8, BOM, CRLF, body-hash drift, missing ingest-log paths, and unregistered importer directories: 0.
- Canonical pages and index entries: 0; no canonical navigation update was required.

## [2026-07-21] create | 2nd-Brain canonical 지식 코어

- Evidence: the existing 13-file raw source set was mapped to eight central, reusable PKM subjects; no raw record was duplicated or mutated.
- Created:
  - `concepts/ai-knowledge-workflow.md`
  - `concepts/ai-personal-knowledge-management.md`
  - `concepts/llm-wiki.md`
  - `concepts/research-feedback-loop.md`
  - `concepts/second-brain-research-workflow.md`
  - `comparisons/knowledge-tool-roles.md`
  - `queries/notebooklm-query-compounding.md`
  - `queries/ua-knowledge-graph-workflow.md`
- Updated:
  - `SCHEMA.md`
  - `index.md`
  - `log.md`
- Navigation: the eight-page graph uses only resolvable canonical wikilinks, with at least two distinct non-self links per page.
- Provenance: every source and claim marker resolves to an existing repository-relative raw Markdown path.

## [2026-07-21] lint | 0 issues found

- Canonical pages: 8 total (5 concepts, 1 comparison, and 2 queries); all required frontmatter fields, types, dates, confidence values, contestation fields, and contradiction lists are valid.
- Taxonomy and navigation: 9 registered tags, 8 exact alphabetical index entries, 33 canonical links, minimum 3 outbound links per page, and minimum 2 inbound links per page.
- Provenance: 27 source references and 17 claim-level markers resolve to existing raw Markdown records; no marker is absent from its page source list.
- Raw integrity: 13 Markdown records checked, 8 recorded body hashes matched, and 5 importer-preserved legacy hash/final-LF coverage gaps remain documented.
- Formatting, duplicate slugs, broken links, self-links, orphan pages, source drift, and lint warnings: 0.

## [2026-07-21] repair | lint source-reference count correction

- Correction: the immediately preceding lint entry reports 27 source references, but the measured canonical frontmatter total is 30.
- Unchanged measurements: 17 claim-level markers, 33 canonical links, 8 canonical pages, and 0 lint errors or warnings.
- Updated: `log.md` only; no raw or canonical page was changed.

## [2026-07-31] update | finance 도메인 스키마 확장

- Evidence: financial 정보를 위한 canonical wiki 확장을 준비하기 위해 스키마에 finance
  도메인 태그와 raw 소스 디렉토리를 등록함. 아직 raw 레코드나 canonical 페이지는
  생성하지 않음 (0건).
- Registered tags: `macro`, `equity`, `earnings`, `filing`, `valuation`, `crypto`,
  `portfolio`.
- Created:
  - `raw/filings/.gitkeep`
  - `raw/earnings/.gitkeep`
- Updated:
  - `SCHEMA.md` (directory role table, registered tag taxonomy)
- Navigation: `index.md` unchanged; canonical page count remains 0.

## [2026-07-31] ingest | Korean stocks record-14% AI trade optimism 뉴스

- Evidence: `inbox/`에 URL 기반 뉴스 기사 1건을 임시 적재한 뒤 분류 테스트를 진행함.
  주제가 개별 뉴스 이벤트(단일 소스)이고 아직 반복 등장하는 두 번째 소스가 없어
  canonical 페이지는 생성하지 않음.
- Source: `https://finance.yahoo.com/markets/stocks/articles/korean-stocks-jump-record-14-000934073.html`
  (Bloomberg, Youkyung Lee, published 2026-07-31).
- Verification: WebFetch 요약본을 원본 HTML(`curl`로 직접 수신)과 대조해 본문·수치가
  실제 게재 기사와 일치함을 확인함 (Kospi +14%, SK Hynix +28%, Samsung +26%는 수치가
  이례적으로 크지만 원문에 실제로 게재된 값임).
- Classified into: `raw/articles/` (tags: `news`, `equity`, `macro`).
- Created:
  - `raw/articles/korean-stocks-jump-record-14pct-ai-optimism.md`
- Deleted:
  - `inbox/korean-stocks-jump-record-14pct-ai-optimism.md` (분류 완료 후 임시 적재분 제거)
- Navigation: `index.md` unchanged; canonical page count remains 0.

## [2026-08-01] lint | finance-morning-digest cron 실행 결과 무결성 이슈

- Scope: 2026-08-01 03:00 KST `finance-morning-digest` cron(job `f7215c8998ff`)
  실행으로 생성된 `raw/articles/` 신규 레코드 2건을 점검.
- Found:
  - `raw/articles/apple-stock-falls-on-weak-revenue-forecast-as-ceo-tim-cook-flags-increasing-impact-from-memory-shortage.md`
  - `raw/articles/stock-market-today-dow-s_p-500_nasdaq-seesaw-as-10-year-yield-surges-big-tech-s.md`
  두 파일 모두 YAML frontmatter(`---`)가 없고 `title/created/tags/sha256`
  등 필수·관례 필드가 누락됨; 대응하는 `log.md` ingest 항목도 이 항목
  이전까지 기록되지 않았음.
- Root cause: `~/.hermes/logs/agent.log` 대조 결과, 크론 에이전트(로컬
  gemma4:12b)가 `execute_code` 호출이 BLOCKED되자 결정론적 처리 스크립트
  `file-article.py`(frontmatter·sha256·log.md 기록 담당)를 `terminal`로
  호출하지 않고 `write_file`로 두 파일을 직접 작성함. 스크립트 자체의
  가드는 무력화되지 않았고, 모델이 스크립트 호출을 생략한 것이 원인.
- Fix status: 이번 항목에서는 두 raw 파일과 스크립트/크론 설정을 수정하지
  않음 — 발견된 상태만 기록.
- Reference: `docs/260801_01_current-system-architecture.md` §5.
- Navigation: `index.md` unchanged; canonical page count remains 0.

## [2026-08-01] ingest | Apple Q3 FY2026 earnings: beat on top/bottom line, stock falls on Services/China miss + memory shortage

- Source: `https://finance.yahoo.com/technology/article/apple-stock-falls-on-weak-revenue-forecast-as-ceo-tim-cook-flags-increasing-impact-from-memory-shortage-130428410.html`
- Status: 검증됨
- Created:
  - `raw/articles/apple-stock-falls-on-weak-revenue-forecast-as-ceo-tim-cook-flags-increasing-impa.md`

## [2026-08-01] ingest | Stock market wrap 2026-07-31: Dow/S&P/Nasdaq up on week despite yield surge, Big Tech AI capex guidance

- Source: `https://finance.yahoo.com/markets/live/stock-market-today-friday-july-31-dow-sp-500-nasdaq-081227738.html`
- Status: 검증됨
- Created:
  - `raw/articles/stock-market-today-dow-s-p-500-nasdaq-seesaw-as-10-year-yield-surges-big-tech-s.md`

## [2026-08-01] repair | 2026-08-01 lint 발견 무결성 이슈 해소 + 파이프라인 재설계

- 대상: 위 `[2026-08-01] lint` 항목에서 발견된 frontmatter/sha256 누락 raw
  레코드 2건.
- 조치: 두 기사 원문(`curl`)을 다시 받아 실제 본문(JSON-LD `articleBody` 또는
  cross-source 대조)을 근거로 Claude Code가 직접 요약을 작성하고,
  `file-article.py`로 재등록함. 기존 malformed 파일은 삭제하고 위 두
  `ingest` 항목의 신규 파일로 대체함 (slug가 달라 파일명 변경됨).
- Deleted:
  - `raw/articles/apple-stock-falls-on-weak-revenue-forecast-as-ceo-tim-cook-flags-increasing-impact-from-memory-shortage.md`
  - `raw/articles/stock-market-today-dow-s_p-500_nasdaq-seesaw-as-10-year-yield-surges-big-tech-s.md`
- 근본 원인 대응: `finance-morning-digest` cron(job `f7215c8998ff`)을
  `hermes cron edit --no-agent`로 전환하고, `~/.hermes/scripts/finance-morning-digest.py`를
  raw/ 직접 기록 대신 `inbox/`에 제목+URL+RSS teaser만 큐잉하도록 재작성함.
  이제 크론 실행에는 LLM 판단이 전혀 개입하지 않으므로(스크립트 자체가
  job), 로컬 모델이 결정론적 스크립트 호출을 건너뛰는 이번 실패 유형은
  구조적으로 재발할 수 없음. `inbox/`에 쌓인 항목은 이후 Claude Code
  세션이 원문을 읽고 직접 요약을 작성해 `file-article.py`로 승격하는
  방식으로 처리함(이번 두 건이 그 절차의 첫 실행 사례).
- Updated:
  - `~/.hermes/scripts/finance-morning-digest.py` (저장소 외부, Hermes 홈)
  - Hermes cron job `f7215c8998ff` (no-agent 모드로 전환)
- Reference: `docs/260801_02_inbox-queue-pipeline-implementation.md`
- Navigation: `index.md` unchanged; canonical page count remains 0.

## [2026-08-01] ingest | Apple x Klarna iPhone leasing program overview

- Source: `https://finance.yahoo.com/personal-finance/banking/article/apples-iphone-leasing-program-how-it-works-what-to-consider-143105471.html`
- Status: 검증됨
- Created:
  - `raw/articles/apple-s-iphone-leasing-program-how-it-works-what-to-consider.md`

## [2026-08-01] ingest | Best CD rates roundup 2026-07-31

- Source: `https://finance.yahoo.com/personal-finance/banking/article/best-cd-rates-today-friday-july-31-2026-up-to-415-apy-return-100000041.html`
- Status: 검증됨
- Created:
  - `raw/articles/best-cd-rates-today-friday-july-31-2026-up-to-4-15-apy-return.md`

## [2026-08-01] ingest | BTC/ETH price snapshot 2026-07-31

- Source: `https://finance.yahoo.com/personal-finance/investing/article/bitcoin-and-ethereum-prices-today-friday-july-31-2026-crypto-prices-back-off-this-morning-130657761.html`
- Status: 검증됨
- Created:
  - `raw/articles/bitcoin-and-ethereum-prices-today-friday-july-31-2026-crypto-prices-back-off-thi.md`

## [2026-08-01] ingest | Gold price breaks $4,100 2026-07-31

- Source: `https://finance.yahoo.com/personal-finance/investing/article/gold-prices-today-friday-july-31-2026-gold-price-finally-breaks-above-4100-as-us-paused-airstrikes-overnight-123436216.html`
- Status: 검증됨
- Created:
  - `raw/articles/gold-prices-today-friday-july-31-2026-gold-price-finally-breaks-above-4-100-as-u.md`

## [2026-08-01] ingest | How to save $5,000 in 6 months (guide)

- Source: `https://finance.yahoo.com/personal-finance/banking/article/how-to-save-5000-in-6-months-203322543.html`
- Status: 검증됨
- Created:
  - `raw/articles/how-to-save-5-000-in-6-months.md`

## [2026-08-01] ingest | Mortgage rates snapshot 2026-07-31

- Source: `https://finance.yahoo.com/personal-finance/mortgages/article/mortgage-and-refinance-interest-rates-today-friday-july-31-2026-mortgage-rates-find-more-room-to-fall-100000678.html`
- Status: 검증됨
- Created:
  - `raw/articles/mortgage-and-refinance-interest-rates-today-friday-july-31-2026-mortgage-rates-f.md`

## [2026-08-01] ingest | Silver price briefly tops $59 2026-07-31

- Source: `https://finance.yahoo.com/personal-finance/investing/article/silver-prices-today-friday-july-31-2026-silver-briefly-rises-above-59-after-us-pauses-airstrikes-124419446.html`
- Status: 검증됨
- Created:
  - `raw/articles/silver-prices-today-friday-july-31-2026-silver-briefly-rises-above-59-after-u-s.md`

## [2026-08-01] ingest | Travel delay insurance coverage overview

- Source: `https://finance.yahoo.com/personal-finance/insurance/article/travel-delay-insurance-150541453.html`
- Status: 검증됨
- Created:
  - `raw/articles/travel-delay-insurance-what-s-covered-and-what-s-not.md`

## [2026-08-01] ingest | 1inch launches Aqua shared-liquidity protocol

- Source: `https://finance.yahoo.com/markets/crypto/articles/want-trade-spacex-apple-1inch-194500911.html`
- Status: 검증됨
- Created:
  - `raw/articles/want-to-trade-spacex-for-apple-1inch-says-skip-the-dollars.md`

## [2026-08-01] update | inbox 9건 일괄 처리 + personal-finance 태그 등록

- Evidence: `docs/260801_02`에서 재설계한 흐름대로, `inbox/finance-*.md` 9건을
  Claude Code가 하나씩 원문 재수신(curl) 후 직접 요약을 작성해
  `file-article.py`로 승격함 (위 9개 `ingest` 항목). Yahoo Finance RSS가
  실제로 반환한 항목이라 CD/모기지 금리, 저축·보험 가이드 등 소비자
  금융 콘텐츠가 다수 포함됨 — 기존 taxonomy(`macro/equity/earnings/
  filing/valuation/crypto/portfolio`)로는 이 유형을 적절히 분류할 수
  없어 `personal-finance` 태그를 신규 등록함(consumer financial products
  and advice, 기관/시장 분석과 구분).
- Registered tags: `personal-finance`.
- Updated:
  - `SCHEMA.md` (Registered tags 목록에 `personal-finance` 추가)
- Classification: `crypto`(2건: BTC/ETH 시세, 1inch), `macro`(2건: 금·은
  시세), `macro`+`personal-finance`(1건: 모기지 금리), `personal-finance`
  (4건: 아이폰 리스, CD 금리, 저축 가이드, 여행자보험).
- Deleted:
  - `inbox/finance-apple-s-iphone-leasing-program-how-it-works-what-to-consider.md`
  - `inbox/finance-best-cd-rates-today-friday-july-31-2026-up-to-4-15-apy-return.md`
  - `inbox/finance-bitcoin-and-ethereum-prices-today-friday-july-31-2026-crypto-prices-back-off-thi.md`
  - `inbox/finance-gold-prices-today-friday-july-31-2026-gold-price-finally-breaks-above-4-100-as-u.md`
  - `inbox/finance-how-to-save-5-000-in-6-months.md`
  - `inbox/finance-mortgage-and-refinance-interest-rates-today-friday-july-31-2026-mortgage-rates-f.md`
  - `inbox/finance-silver-prices-today-friday-july-31-2026-silver-briefly-rises-above-59-after-u-s.md`
  - `inbox/finance-travel-delay-insurance-what-s-covered-and-what-s-not.md`
  - `inbox/finance-want-to-trade-spacex-for-apple-1inch-says-skip-the-dollars.md`
- Note: 모든 9건이 RSS teaser/og:description만 확보되고 전체 본문은
  접근 불가했음(`docs/260731_05`에서 기록된 동일한 Yahoo SPA 제약).
  Canonical 승격은 보류 — 각 주제가 아직 단일 소스임.
- Navigation: `index.md` unchanged; canonical page count remains 0.
