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

## [2026-08-01] ingest | CD rates Aug 1 2026

- Source: `https://finance.yahoo.com/personal-finance/banking/article/best-cd-rates-today-saturday-august-1-2026-best-cd-account-earns-415-apy-100000014.html`
- Status: 검증됨
- Created:
  - `raw/articles/best-cd-rates-today-saturday-august-1-2026-best-cd-account-earns-4-15-apy.md`

## [2026-08-01] ingest | Mortgage rates Aug 1 2026

- Source: `https://finance.yahoo.com/personal-finance/mortgages/article/mortgage-and-refinance-interest-rates-today-saturday-august-1-2026-rates-higher-than-friday-100000052.html`
- Status: 검증됨
- Created:
  - `raw/articles/mortgage-and-refinance-interest-rates-today-saturday-august-1-2026-rates-higher.md`

## [2026-08-01] ingest | BYD overseas sales flash charging

- Source: `https://www.investors.com/news/tesla-rival-byd-sales-overseas-demand-flash-charging/?src=A00220&yptr=yahoo`
- Status: 미검증
- Created:
  - `raw/articles/tesla-rival-byd-ramping-up-sales-on-overseas-demand-flash-charging.md`

## [2026-08-01] update | finance-inbox-promote 자동화(Kimi K2/OpenRouter) 구축

- Evidence: `docs/260801_04`에서 추정한 모델/비용을 바탕으로 `inbox/` →
  `raw/articles/` 승격(2단계 B)을 자동화하는 Hermes cron job을 새로 만들고
  실제 기사 3건으로 종단 검증함. 위 3건의 `ingest` 항목이 이 job의 검증
  실행 결과물이다.
- Created (저장소 외부, Hermes 홈):
  - `~/.hermes/scripts/fetch-article-excerpt.py` (원문에서 텍스트만 추출,
    raw HTML 전체를 에이전트 컨텍스트에 넣지 않기 위함)
  - Hermes cron job `9e11da6aa541` (`finance-inbox-promote`, `30 3 * * *`,
    `--provider openrouter --model moonshotai/kimi-k2-0905`, agent 모드)
- Found + Fixed: 검증 실행 중 inbox 정리 단계(`rm`)가 Hermes 자체 보안
  스캐너("Mass file deletion in a short window")에 차단됨 — raw 등록
  자체는 3건 모두 성공했으나 inbox 파일은 지워지지 않았고, 모델이 이
  실패를 Discord 보고에 정확히 남김. 조치: 프롬프트를 `rm` 대신
  `inbox/.processed/`로 `mv`하도록 수정. 이번 실행에서 남은 3개 inbox
  파일은 수동으로 `inbox/.processed/`에 이동 처리함.
- Cost 실측: 빈 inbox 실행 ≈ $0.019, 기사 3건 처리 ≈ $0.153(건당 ≈
  $0.051, `docs/260801_04` 사전 추정 $0.075보다 낮음 — 프롬프트 캐싱
  효과로 추정).
- Reference: `docs/260801_05_finance-inbox-promote-automation.md`
- Navigation: `index.md` unchanged; canonical page count remains 0.

## [2026-08-02] ingest | Car Loan Burden

- Source: `https://finance.yahoo.com/markets/stocks/articles/1-5-car-buyers-stuck-142500536.html`
- Status: 검증됨
- Created:
  - `raw/articles/1-in-5-new-car-buyers-are-stuck-in-a-000-a-month-nightmare-and-it-s-ruining-thei.md`

## [2026-08-02] ingest | Best CD Rates

- Source: `https://finance.yahoo.com/personal-finance/banking/article/best-cd-rates-today-saturday-august-1-2026-best-cd-account-earns-410-apy-100000014.html`
- Status: 검증됨
- Created:
  - `raw/articles/best-cd-rates-today-saturday-august-1-2026-best-cd-account-earns-4-10-apy.md`

## [2026-08-02] ingest | Dow Jones Futures

- Source: `https://www.investors.com/market-trend/stock-market-today/dow-jones-futures-spacex-amd-sandisk-eli-lilly-earnings-loom/?src=A00220&yptr=yahoo`
- Status: 미검증
- Created:
  - `raw/articles/dow-jones-futures-market-rebounds-now-watch-for-this-spacex-amd-sandisk-eli-lill.md`

## [2026-08-02] ingest | GE Aerospace Stocks

- Source: `https://www.investors.com/news/ge-aerospace-ai-play-netapp-lead-5-stocks-near-buy-points/?src=A00220&yptr=yahoo`
- Status: 미검증
- Created:
  - `raw/articles/ge-aerospace-ai-play-lead-five-stocks-near-buy-points.md`

## [2026-08-02] ingest | Gold vs Silver ETF

- Source: `https://finance.yahoo.com/markets/commodities/articles/gold-trust-vs-silver-trust-171701717.html`
- Status: 검증됨
- Created:
  - `raw/articles/gold-trust-vs-silver-trust-which-precious-metal-etf-should-win-investor-dollars.md`

## [2026-08-02] ingest | Reddit Stock

- Source: `https://finance.yahoo.com/markets/stocks/articles/google-traffic-wobble-sends-major-170700469.html`
- Status: 검증됨
- Created:
  - `raw/articles/google-traffic-wobble-sends-major-signal-for-sinking-reddit-stock.md`

## [2026-08-02] ingest | HSA Retirement Tool

- Source: `https://finance.yahoo.com/healthcare/articles/health-savings-accounts-great-retirement-212800955.html`
- Status: 검증됨
- Created:
  - `raw/articles/health-savings-accounts-can-be-a-great-retirement-tool-if-you-re-healthy-or-weal.md`

## [2026-08-02] ingest | Grail Stock Analysis

- Source: `https://finance.yahoo.com/markets/stocks/articles/grail-gral-stock-buy-sell-172820956.html`
- Status: 검증됨
- Created:
  - `raw/articles/is-grail-gral-stock-a-buy-sell-or-hold-at-under-0.md`

## [2026-08-02] ingest | Fed Rate Outlook

- Source: `https://finance.yahoo.com/economy/policy/articles/j-p-morgan-drops-fed-060300978.html`
- Status: 검증됨
- Created:
  - `raw/articles/j-p-morgan-drops-fed-rate-bombshell-over-warsh-inflation.md`

## [2026-08-02] ingest | Home Repair Costs

- Source: `https://finance.yahoo.com/real-estate/articles/nearly-75-homeowners-spend-10-123000374.html`
- Status: 검증됨
- Created:
  - `raw/articles/nearly-75-of-new-homeowners-spend-0-000-on-surprise-repairs-within-2-years-and-s.md`

## [2026-08-02] ingest | Dalio Asset Warning

- Source: `https://finance.yahoo.com/markets/currencies/articles/ray-dalio-warns-major-asset-125500604.html`
- Status: 검증됨
- Created:
  - `raw/articles/ray-dalio-warns-this-major-asset-will-have-the-worst-return-guaranteed-and-you-p.md`

## [2026-08-02] ingest | Kiyosaki Crash Warning

- Source: `https://finance.yahoo.com/markets/stocks/articles/robert-kiyosaki-warns-boomers-set-121000989.html`
- Status: 검증됨
- Created:
  - `raw/articles/robert-kiyosaki-warns-boomers-are-set-up-for-a-historic-rug-pull-and-will-end-up.md`

## [2026-08-02] ingest | IRA Abroad Rules

- Source: `https://finance.yahoo.com/markets/currencies/articles/2-irs-rules-allow-continue-133000736.html`
- Status: 검증됨
- Created:
  - `raw/articles/the-2-irs-rules-that-allow-you-to-continue-making-ira-contributions-when-you-mov.md`

## [2026-08-02] ingest | Travel Money Traps

- Source: `https://finance.yahoo.com/small-business/articles/5-travel-money-traps-avoid-130000525.html`
- Status: 검증됨
- Created:
  - `raw/articles/the-5-travel-money-traps-to-avoid-according-to-someone-who-has-visited-nearly-10.md`

## [2026-08-02] ingest | Bank of England Coal

- Source: `https://finance.yahoo.com/economy/policy/articles/bank-england-moving-away-coal-150000057.html`
- Status: 검증됨
- Created:
  - `raw/articles/the-bank-of-england-is-moving-away-from-coal.md`

## [2026-08-02] ingest | Fallen Angel Bond Fund

- Source: `https://finance.yahoo.com/markets/options/articles/fallen-angel-bond-fund-pays-170754302.html`
- Status: 검증됨
- Created:
  - `raw/articles/the-fallen-angel-bond-fund-pays-6-5-and-has-beaten-the-biggest-junk-fund-for-a-d.md`

## [2026-08-02] ingest | Archer Aviation Stock

- Source: `https://finance.yahoo.com/markets/stocks/articles/aerospace-stock-cheap-does-buy-173500686.html`
- Status: 검증됨
- Created:
  - `raw/articles/this-aerospace-stock-is-cheap-but-does-that-make-it-a-buy-today.md`

## [2026-08-02] ingest | Buffett Warning

- Source: `https://finance.yahoo.com/markets/stocks/articles/warren-buffetts-berkshire-hathaway-sounding-173000045.html`
- Status: 검증됨
- Created:
  - `raw/articles/warren-buffett-s-berkshire-hathaway-is-sounding-a-warning-what-history-tells-us.md`

## [2026-08-02] update | finance-morning-digest에 CNBC RSS 4종 추가

- Evidence: Yahoo Finance RSS 단독으로는 CD/모기지 금리, 여행자보험 같은
  개인재무 뉴스 비중이 높아 "중요한 기사만" 가져오고 싶다는 요청에 따라
  뉴스 소스를 다각화함. CNBC RSS 후보 7개를 `curl`로 검증한 결과 6개가
  정상 응답(economy/finance/markets/business/top-news/investing), 1개
  (`id/15839263`, "earnings"로 추정했던 ID)는 실제로는 비디오 피드라 제외.
  매크로/기업 초점에 맞는 4개만 채택하고 general 성격의 top-news·investing은
  제외함.
- Updated (저장소 외부, Hermes 홈):
  - `~/.hermes/scripts/finance-morning-digest.py` — 단일 `RSS_URL` 문자열을
    `RSS_FEEDS` 딕셔너리(yahoo + cnbc-economy/finance/markets/business)로
    교체, 피드별 개별 실패를 허용(`fetch_all_feeds`가 개별 feed 예외를
    잡아 나머지는 계속 진행), inbox 항목에 `feed` 필드 추가, 같은 실행 내
    중복 링크 가드(`seen_this_run`) 추가.
- Verification: 수동 실행으로 CNBC 기사 3건이 정상 큐잉됨을 확인
  (Goldman traders, Berkshire Hathaway, Best Buy CEO 전략 — Yahoo
  단독일 때보다 기관/기업 관련도가 높은 기사들).
- Navigation: `index.md` unchanged; canonical page count remains 0.

## [2026-08-02] update | data/ 레이어 신설 — FRED 매크로 + SEC 재무 시계열 수집

- Evidence: `docs/260802_01_Knowledge-Base.md`("뉴스 20% : 구조화 데이터
  80%")를 실행에 옮기는 첫 단계. 워치리스트는 우선 NVDA, TSLA로 시작
  (사용자가 이후 하나씩 추가 요청 예정). FRED_API_KEY는 사용자가
  `~/.hermes/.env`에 직접 등록; Alpha Vantage/FMP(밸류에이션 배수용)는
  아직 미보유 — 이번 단계에서는 키 없이 가능한 FRED·SEC EDGAR만 구축.
- Schema change: `SCHEMA.md`에 `data/` 레이어를 신설(raw의 불변/sha256
  계약과 별개— 계속 갱신되는 구조화 시계열이라 성격이 다름을 명시).
  `data/macro/`, `data/companies/<TICKER>/` 디렉토리 역할 등록.
- Created (저장소 내부):
  - `data/macro/*.csv` (FRED Tier 1 지표 13종, 각 최대 3년치 초기 적재)
  - `data/companies/NVDA/financials.csv`, `data/companies/TSLA/financials.csv`
    (SEC XBRL 기반 분기/연간 재무제표 시계열)
- Created (저장소 외부, Hermes 홈):
  - `~/.hermes/scripts/fetch-fred-macro.py` — FRED API로 매크로 지표
    수집, 기존 CSV 마지막 날짜 이후만 증분 추가.
  - `~/.hermes/scripts/fetch-sec-financials.py` — SEC EDGAR
    `companyfacts` API(키 불필요, User-Agent만 필요)로 워치리스트
    티커의 재무제표 항목(매출/매출총이익/영업이익/순이익/EPS/영업현금흐름/
    CapEx/R&D/장기부채) 추출.
- Hermes cron 신설 (전부 `--no-agent`, LLM 호출 없음, 결정론적):
  - `4e742a6edf84` (`fred-macro-fetch`, `0 2 * * *`)
  - `087f14e755d7` (`sec-financials-fetch`, `10 2 * * *`)
- Known gaps: ISM 제조업/서비스업 PMI, GDPNow는 FRED 무료 API로 더 이상
  제공되지 않아 Tier 1 목표 16종 중 13종만 확보(문서화된 gap, 대체
  소스 필요 시 별도 검토). Gold/Copper/Bitcoin 같은 Tier 2 상품·자산은
  FRED에 신뢰할 만한 무료 시계열이 없어 이번 단계에서 제외.
- Verification: 두 스크립트 모두 최초 실행으로 정상 데이터 확보(예:
  T10Y2Y 최신값 +0.47로 비역전 상태, NVDA FY2026 매출 $215.9B, TSLA
  FY2025 매출 $94.8B) — 임의 값이 아닌 실제 FRED/SEC 응답임을 raw JSON
  대조로 확인.
- Reference: `docs/260802_02_macro-financial-data-layer.md`
- Navigation: `index.md` unchanged; canonical page count remains 0.

## [2026-08-03] ingest | Berkshire Alphabet Position

- Source: `https://finance.yahoo.com/markets/stocks/articles/3-reasons-why-berkshire-hathaway-165000908.html`
- Status: 검증됨
- Created:
  - `raw/articles/3-reasons-why-berkshire-hathaway-owns-9-billion-of-alphabet-stock.md`

## [2026-08-03] ingest | Amazon Debt and AI Spending

- Source: `https://finance.yahoo.com/markets/stocks/articles/amazons-debt-nearly-doubled-129-140000968.html`
- Status: 검증됨
- Created:
  - `raw/articles/amazon-s-debt-nearly-doubled-to-29-billion-in-6-months-as-ceo-jassy-defends-20-b.md`

## [2026-08-03] ingest | SpaceX Pre-Earnings Signal

- Source: `https://finance.yahoo.com/markets/stocks/articles/analyst-sends-strong-signal-spacex-173300981.html`
- Status: 검증됨
- Created:
  - `raw/articles/analyst-sends-strong-signal-on-spacex-stock-before-earnings.md`

## [2026-08-03] ingest | Microsoft Cloud Revenue Analysis

- Source: `https://finance.yahoo.com/markets/stocks/articles/cloud-revenue-soars-time-buy-163500803.html`
- Status: 검증됨
- Created:
  - `raw/articles/as-cloud-revenue-soars-is-it-time-to-buy-microsoft-stock.md`

## [2026-08-03] ingest | BofA Apple Bullish Outlook

- Source: `https://finance.yahoo.com/markets/stocks/articles/bank-america-doubles-down-apple-170700925.html`
- Status: 검증됨
- Created:
  - `raw/articles/bank-of-america-doubles-down-on-apple-stock-for-rest-of-2026.md`

## [2026-08-03] ingest | Berkshire 8-Month High

- Source: `https://www.cnbc.com/2026/08/01/-berkshire-hathaway-shares-hit-eight-month-high.html`
- Status: 미검증
- Created:
  - `raw/articles/berkshire-hathaway-shares-hit-eight-month-high.md`

## [2026-08-03] ingest | Best CD Rates Today

- Source: `https://finance.yahoo.com/personal-finance/banking/article/best-cd-rates-today-sunday-august-2-2026-lock-in-up-to-410-apy-100000506.html`
- Status: 검증됨
- Created:
  - `raw/articles/best-cd-rates-today-sunday-august-2-2026-lock-in-up-to-4-10-apy.md`

## [2026-08-03] ingest | Bloom vs Oklo Comparison

- Source: `https://finance.yahoo.com/energy/articles/bloom-energy-vs-oklo-power-172001626.html`
- Status: 검증됨
- Created:
  - `raw/articles/bloom-energy-vs-oklo-which-power-stock-is-a-better-buy-in-2026.md`

## [2026-08-03] ingest | Carmelo Contract Breakdown

- Source: `https://finance.yahoo.com/small-business/articles/carmelo-anthony-breaks-down-100m-140000809.html`
- Status: 검증됨
- Created:
  - `raw/articles/carmelo-anthony-breaks-down-how-a-00m-contract-shrinks-to-under-0m-and-where-the.md`

## [2026-08-03] ingest | Cathie Wood Snowflake Sale

- Source: `https://finance.yahoo.com/markets/stocks/articles/cathie-wood-sells-5-5-163300469.html`
- Status: 검증됨
- Created:
  - `raw/articles/cathie-wood-sells-5-million-of-surging-tech-stock.md`

## [2026-08-03] ingest | Goldman Traders Record Year

- Source: `https://www.cnbc.com/2026/08/01/goldman-traders-are-on-pace-for-a-record-year-a-close-up-look-at-how-theyre-doing-it.html`
- Status: 미검증
- Created:
  - `raw/articles/goldman-traders-are-on-pace-for-a-record-year-a-close-up-look-at-how-they-re-doi.md`

## [2026-08-03] ingest | Morgan Stanley Crypto ETFs

- Source: `https://finance.yahoo.com/markets/crypto/articles/morgan-stanley-just-launched-ethereum-172400392.html`
- Status: 검증됨
- Created:
  - `raw/articles/morgan-stanley-just-launched-new-ethereum-and-solana-etfs-here-s-what-it-could-m.md`

## [2026-08-03] ingest | Mortgage Rates Aug 2

- Source: `https://finance.yahoo.com/personal-finance/mortgages/article/mortgage-and-refinance-interest-rates-today-sunday-august-2-2026-rates-a-bit-lower-than-last-week-100000673.html`
- Status: 검증됨
- Created:
  - `raw/articles/mortgage-and-refinance-interest-rates-today-sunday-august-2-2026-rates-a-bit-low.md`

## [2026-08-03] ingest | Ramit Sethi Debt Counseling

- Source: `https://finance.yahoo.com/small-business/articles/ramit-sethi-helps-newlyweds-tackle-133000103.html`
- Status: 검증됨
- Created:
  - `raw/articles/ramit-sethi-helps-newlyweds-tackle-65-000-in-debt-including-the-0-000-he-hid-bef.md`

## [2026-08-03] ingest | Semiconductor Sell-Off Strategy

- Source: `https://finance.yahoo.com/markets/stocks/articles/semiconductor-sell-off-1-chip-170500118.html`
- Status: 검증됨
- Created:
  - `raw/articles/semiconductor-sell-off-1-chip-stock-to-buy-1-to-hold-and-1-to-sell.md`

## [2026-08-03] update | Discord 봇 인증/채널 설정 수정 (경제 지식 퀴즈 사전 준비)

- Evidence: "매일 새벽 지식+퀴즈를 Discord로" 기능을 만들기 전에 "답장이
  실제로 인식되는지" 시범 테스트를 진행하다가 Hermes 게이트웨이의
  Discord 인증 설정이 두 군데 다 잘못돼 있음을 발견해 수정함
  (`data/`, `raw/`, 위키 canonical과 무관, Hermes 홈 설정만 변경).
- Found + Fixed (저장소 외부, `~/.hermes/.env`):
  1. `DISCORD_ALLOWED_USERS=2nd-brain` — 실제 사용자가 아니라 봇 자기
     자신의 이름이 들어가 있어 모든 사용자 메시지가 조용히 차단됨.
     → 사용자 실제 Discord 숫자 ID(`1059828403110428834`)로 교체.
     (중간에 사용자명 문자열(`seongjun_choi`)로 먼저 바꿨다가, 게이트웨이
     레벨의 별도 인증 체크(`gateway/authz_mixin.py`)가 사용자명 해석 없이
     원시 문자열을 숫자 ID와 비교한다는 걸 확인하고 숫자 ID로 재수정 —
     어댑터 레벨 체크와 게이트웨이 레벨 체크 두 겹이라 사용자명 방식은
     구조적으로 항상 실패했음.)
  2. `DISCORD_FREE_RESPONSE_CHANNELS` 미설정 — 멘션 없는 일반 답장은
     기본적으로 무시됨. → 크론 배달 채널(`1532595343110307900`)을 등록해
     멘션 없이도 반응하도록 함.
  3. `DISCORD_ALLOWED_CHANNELS`, `DISCORD_HOME_CHANNEL`을 둘 다
     `1532595343110307900`로 설정 — 봇이 이 채널에서만 반응하도록 제한
     (기존 홈 채널 `1224598309566418966`에서 변경).
- Verification: 위 수정 후 실제 멘션 없는 답장이 정상 인식되고 봇이
  응답함을 확인함(로그: `inbound message: ... msg='...' ` → 정상 응답 전달).
- Navigation: `index.md` unchanged; canonical page count remains 0.

## [2026-08-03] update | econ-daily-lesson 크론 신설 (경제 지식 퀴즈)

- Evidence: Discord 인증 수정이 검증된 뒤, "매일 새벽 지식 하나 + 어제
  퀴즈"를 자동화하는 크론을 구축함. 쉬운 개념부터 차근차근이라는 요청에
  따라 15개 주제로 구성된 고정 커리큘럼(매크로 사이클 → 밸류에이션
  순서)을 만들고, 진도 관리는 결정론적 스크립트가, 실제 설명/퀴즈 문구
  작성은 Kimi K2가 담당하도록 역할을 분리함(기존 finance 파이프라인과
  동일한 원칙).
- Created (저장소 외부, Hermes 홈):
  - `~/.hermes/scripts/econ-curriculum.json` — 고정 15주제 커리큘럼(주제명
    + 힌트), 매크로 사이클(채권/금리/인플레이션/고용/GDP/VIX/신용스프레드)
    5~9번, 밸류에이션(P/E/EV-EBITDA/재무제표/FCF) 10~13번, 섹터로테이션
    14번, 종합 15번 순서.
  - `~/.hermes/scripts/advance-econ-lesson.py` — 결정론적 진도 관리:
    `~/.hermes/state/econ-quiz-state.json`의 `curriculum_index`를 매 실행마다
    +1(15 완료 시 순환), 오늘/어제 주제를 JSON으로 출력해 에이전트
    프롬프트에 주입.
  - `~/.hermes/state/econ-quiz-state.json` — 진도 상태(현재 index 0, 1/15
    학습 완료).
- Hermes cron 신설: `3d03d50a2cf6` (`econ-daily-lesson`, `20 2 * * *`,
  `--script advance-econ-lesson.py`, agent 모드, `--provider openrouter
  --model moonshotai/kimi-k2-0905`).
- Verification: 수동 1회 실행 — "채권 가격과 금리의 역관계"를 쉬운 예시와
  함께 정상 설명, 첫 실행이라 퀴즈는 생략하고 안내 문구만 정상 출력됨을
  확인. API 호출 1회, 입력 15,508 / 출력 460 토큰(비용 미미).
- Note: 실제 답장에 대한 채점/후속 질문은 이 크론이 아니라 상시 실행 중인
  Discord 라이브 챗(로컬 `gemma4:12b`, 기본 모델)이 채널 대화 맥락을 보고
  처리함 — 별도 상태 연동 없이 Discord 채널 히스토리 자체가 맥락 역할을
  함. 채점 품질이 기대에 못 미치면 라이브 챗 모델도 별도로 바꾸는 것을
  고려할 것.
- Navigation: `index.md` unchanged; canonical page count remains 0.
