# 매크로/기업 재무 구조화 데이터 레이어 구축 (FRED + SEC EDGAR)

**작성일**: 2026-08-02
**작성자**: Claude Code
**목적**: `docs/dev-log/260802_01_Knowledge-Base.md`("뉴스는 20%, 구조화 데이터는
80%")를 실제로 구현하는 1단계. 매크로 사이클 판단(목표 1)과 종목 밸류에이션
판단(목표 2)에 필요한 구조화 데이터를 키 없이/무료로 확보 가능한 소스부터
채웠다.

---

## 1. 왜 raw/가 아니라 새 `data/` 레이어인가

`SCHEMA.md`의 raw/ 계약은 "캡처 1건 = 불변 문서 1개 + sha256"을 전제한다.
그런데 FRED 지표나 SEC 재무 항목은 **같은 스크립트를 매일 다시 돌려서 계속
새 값을 이어붙이는** 시계열이라, 이 모델과 근본적으로 안 맞는다(매일 별도
불변 md 파일을 만들면 1년에 지표당 365개 파일이 생긴다). 그래서 raw/를
건드리지 않고 `SCHEMA.md`에 `data/` 레이어를 새로 정의했다 — CSV, append-only,
해시 계약 없음, canonical `sources`로 인용하지 않음(대신 canonical 페이지
본문에 "어떤 시계열을 언제까지 썼는지" 프로즈로 설명).

## 2. 만든 것

### 2.1 `data/macro/` — FRED 매크로 지표

`~/.hermes/scripts/fetch-fred-macro.py`가 FRED 공식 API(`FRED_API_KEY`,
사용자가 `.env`에 직접 등록)로 시리즈별 CSV를 관리한다. 기존 CSV의 마지막
날짜 이후 값만 증분 추가하는 방식이라, 매일 돌려도 중복이 쌓이지 않는다.

`docs/dev-log/260802_01`의 Tier 1 16종 중 13종을 실제로 검증 후 확보:

| 확보됨 | 시리즈 ID |
| --- | --- |
| Fed Funds Rate | `FEDFUNDS` |
| 10Y / 2Y Treasury | `DGS10` / `DGS2` |
| 10Y-2Y Spread | `T10Y2Y` |
| CPI / Core CPI | `CPIAUCSL` / `CPILFESL` |
| PCE | `PCEPI` |
| Nonfarm Payroll | `PAYEMS` |
| Unemployment Rate | `UNRATE` |
| Initial Jobless Claims | `ICSA` |
| Retail Sales | `RSAFS` |
| High Yield Spread | `BAMLH0A0HYM2` |
| VIX | `VIXCLS` |

**확보 못한 3종(문서화된 gap)**: ISM 제조업/서비스업 PMI는 ISM이 2016년경
FRED 무료 배포를 중단해 더 이상 없음. GDPNow는 애틀랜타 연은 자체 상품이라
애초에 FRED에 없음. 대체가 필요하면 유료 소스나 다른 방식을 별도 검토해야
한다. Gold/Copper/Bitcoin 등 Tier 2 상품 시세도 FRED에 신뢰할 만한 무료
시계열이 없어 이번 단계에서 제외했다(Yahoo Finance 시세 스크래핑 등 다른
경로가 필요).

### 2.2 `data/companies/<TICKER>/financials.csv` — SEC 재무제표

`~/.hermes/scripts/fetch-sec-financials.py`가 SEC EDGAR의 `companyfacts`
XBRL API(키 불필요, `User-Agent`만 필요)에서 워치리스트 종목의 재무 항목을
분기/연간 단위로 추출한다: revenue, gross_profit, operating_income,
net_income, eps_diluted, operating_cash_flow, capex, rd_expense,
long_term_debt.

**워치리스트**: 현재 NVDA, TSLA만 (`TICKERS` 딕셔너리에 한 줄 추가하면
확장 — 사용자가 요청하면 그때 추가).

**알려진 데이터 품질 이슈**: XBRL의 "duration" 항목(매출 등, 기간에 대한
값)과 "instant" 항목(장기부채 등, 특정 시점 값)이 SEC의 fy/fp 라벨링
방식 차이로 가끔 별도 행으로 쪼개져 일부 필드만 채워진 sparse row가
생긴다(NVDA 데이터에서 1건 관측). 원본 XBRL 구조 자체의 특성이라, 이번
단계에서는 고치지 않고 알려진 제약으로만 기록한다.

## 3. Hermes cron 신설 (전부 no-agent, LLM 비용 0)

| Job | 스케줄 | 역할 |
| --- | --- | --- |
| `fred-macro-fetch` (`4e742a6edf84`) | `0 2 * * *` | FRED 지표 증분 수집 |
| `sec-financials-fetch` (`087f14e755d7`) | `10 2 * * *` | SEC 재무 항목 증분 수집 |

`finance-morning-digest`(03:00)/`finance-inbox-promote`(03:30)와 동일하게
결정론적 스크립트만 실행 — 판단이 필요 없는 순수 데이터 수집이라 LLM을
아예 개입시키지 않았다(비용 0, 오염 위험 0).

## 4. 검증

두 스크립트를 직접 실행해 초기 데이터를 적재하고 실제 값을 확인:

- `T10Y2Y` 최신값(2026-07-31) = **+0.47** — 장단기 금리 역전 없음(경기
  후퇴 직전 신호는 아직 아님).
- `UNRATE`는 4.4%(2026-02) → 4.2%(2026-06)로 완만히 하락.
- `VIXCLS`는 17~20 구간 — 시장 심리는 비교적 안정적.
- NVDA FY2026(2026-01-25 마감) 매출 **$215.9B**, TSLA FY2025 매출
  **$94.8B** — SEC 원본 JSON과 대조해 실제 응답값임을 확인(추정치 아님).

## 5. 아직 안 한 것 (다음 단계)

1. **밸류에이션 배수**(P/E, EV/EBITDA, 시가총액 등)는 실시간 주가가
   필요한데 FRED/SEC 둘 다 이걸 주지 않는다 — Alpha Vantage 또는
   Financial Modeling Prep API 키가 여전히 필요하다.
2. **매크로 사이클 판단 문서**(`concepts/macro-cycle.md` 같은 살아있는
   해석 페이지)는 아직 안 만듦 — 데이터만 쌓았고, "지금이 Expansion/Late
   Cycle/Recession 중 어디냐"는 해석은 사람 또는 Claude Code가 나중에
   `data/macro/*.csv`를 읽고 작성해야 한다.
3. **Earnings Call Transcript**는 무료 소스가 마땅치 않음 — SEC 8-K의
   실적발표 보도자료(Exhibit 99.1)를 대체재로 쓸지 검토 필요.
4. ISM PMI/GDPNow 대체 소스, Tier 2 상품·자산 시세 소스는 미정.

## 6. 참고

- 전체 계획: `docs/dev-log/260802_01_Knowledge-Base.md`
- 데이터 계약: `SCHEMA.md` "Data layer" 섹션
