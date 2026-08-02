질문의 목표를 보면 단순한 **뉴스 아카이브**가 아니라 **투자 판단을 위한 Knowledge Base**를 만들고 싶은 것입니다.

그렇다면 저는 **"뉴스는 20%, 구조화된 데이터는 80%"** 정도의 비중을 추천합니다.

---

# 목표 1. 매크로 사이클 판단

뉴스보다 훨씬 중요한 것은 경제지표입니다.

## ⭐ Tier 1 (반드시 수집)

이것만 있어도 경기 사이클을 상당히 잘 판단할 수 있습니다.

| 분야  | 지표                     | 업데이트    |
| --- | ---------------------- | ------- |
| 금리  | Fed Funds Rate         | FOMC    |
| 금리  | 10Y Treasury           | Daily   |
| 금리  | 2Y Treasury            | Daily   |
| 금리  | 10Y-2Y Spread          | Daily   |
| 물가  | CPI                    | Monthly |
| 물가  | Core CPI               | Monthly |
| 물가  | PCE                    | Monthly |
| 노동  | Nonfarm Payroll        | Monthly |
| 노동  | Unemployment Rate      | Monthly |
| 노동  | Initial Jobless Claims | Weekly  |
| 제조업 | ISM Manufacturing PMI  | Monthly |
| 서비스 | ISM Services PMI       | Monthly |
| 소비  | Retail Sales           | Monthly |
| 경기  | GDPNow                 | Weekly  |
| 금융  | High Yield Spread      | Daily   |
| 금융  | VIX                    | Daily   |

이 정도만 있어도

> 지금이
>
> * Expansion
> * Late Cycle
> * Slowdown
> * Recession
> * Recovery

정도는 상당히 높은 신뢰도로 판단할 수 있습니다.

---

## ⭐ Tier 2

시장 심리를 위해

* Dollar Index (DXY)
* Brent
* WTI
* Gold
* Copper
* Bitcoin
* S&P500
* Nasdaq100

도 매일 저장하면 좋습니다.

---

## 추천 Source

### FRED

가장 추천합니다.

이유

* API 존재
* 무료
* 신뢰도 최고
* 시계열 관리 편함

---

# 목표 2. 특정 산업 밸류에이션

여기는 뉴스보다

**실적 + 공시 + 컨센서스**

가 거의 전부입니다.

---

## 반드시 수집할 것

### Earnings Call

* Transcript
* Summary

---

### SEC Filing

* 10-Q
* 10-K
* 8-K

---

### Financial Statement

분기마다

```
Revenue

Gross Margin

Operating Margin

EPS

FCF

Net Income

CapEx

Debt
```

---

### Valuation

매일

```
Market Cap

Enterprise Value

P/E

Forward P/E

EV/EBITDA

P/S

PEG

Dividend Yield
```

---

### Estimate

```
EPS Estimate

Revenue Estimate

Next Quarter Estimate

Target Price

Recommendation
```

---

# 어떤 Source를 추천하냐?

제가 추천하는 순위입니다.

## ⭐⭐⭐⭐⭐ SEC EDGAR

가장 중요합니다.

공시는 가장 신뢰도가 높습니다.

---

## ⭐⭐⭐⭐⭐ Earnings Call Transcript

CEO의 생각이 그대로 들어갑니다.

예를 들면

```
AI demand

Pricing

Inventory

China

Tariff

CapEx
```

같은 키워드를 추적하기 좋습니다.

---

## ⭐⭐⭐⭐⭐ Alpha Vantage

무료 API가 있습니다.

가져오기 쉬운 것

* Income Statement
* Balance Sheet
* Cash Flow
* Earnings

---

## ⭐⭐⭐⭐⭐ Financial Modeling Prep

무료 플랜도 꽤 좋습니다.

특히

```
Ratios

DCF

Growth

Historical Valuation
```

등이 편합니다.

---

## ⭐⭐⭐⭐ Polygon

가격 데이터

거래량

옵션

등

---

## ⭐⭐⭐⭐ Finnhub

API가 매우 좋습니다.

```
Recommendation

Insider

Institution

Estimate
```

등 제공

---

# 뉴스는 무엇을 가져올까?

뉴스는 많이 가져올 필요가 없습니다.

저라면

## Reuters

★★★★★

---

## Bloomberg

★★★★★

---

## WSJ

★★★★☆

---

## Yahoo Finance

★★★★☆

---

## CNBC

★★★★☆

---

## Financial Times

★★★★☆

---

이 정도만 가져옵니다.

---

# Sector Rotation까지 하고 싶다면

매일 ETF도 저장합니다.

```
SPY
QQQ

XLK
XLF
XLV
XLE
XLI
XLP
XLY
XLRE
XLU
XLB
XLC
```

그러면

```
Technology

Healthcare

Financial

Energy

Utilities
```

섹터 로테이션도 분석 가능합니다.

---

# 최종적으로 추천하는 크롤링 구조

```text
finance/

├── macro/
│   ├── fred/
│   ├── fed/
│   ├── treasury/
│   ├── pmi/
│   ├── cpi/
│   └── jobs/
│
├── market/
│   ├── indices/
│   ├── commodities/
│   ├── crypto/
│   └── volatility/
│
├── companies/
│   ├── AAPL/
│   │    ├── filings/
│   │    ├── earnings/
│   │    ├── valuation/
│   │    └── news/
│   ├── NVDA/
│   └── ...
│
├── sectors/
│   ├── semiconductors/
│   ├── ai/
│   ├── software/
│   └── healthcare/
│
├── news/
│   ├── reuters/
│   ├── yahoo/
│   ├── bloomberg/
│   └── cnbc/
│
└── concepts/
    ├── macro-cycle.md
    ├── valuation-framework.md
    └── sector-rotation.md
```

## 연구·투자 목적이라면 제가 가장 추천하는 우선순위는 다음과 같습니다.

1. **FRED 경제지표**(경기 사이클 판단의 핵심)
2. **SEC EDGAR 공시**(가장 신뢰도 높은 기업 정보)
3. **Earnings Call Transcript/Summary**(경영진의 질적 정보)
4. **Financial Modeling Prep 또는 Alpha Vantage**(재무제표·밸류에이션 지표)
5. **Reuters 뉴스**(거시경제·기업 이벤트)
6. **Yahoo Finance 뉴스**(보조 소스)

이렇게 구성하면 단순히 "오늘 무슨 뉴스가 있었는지"를 모으는 시스템이 아니라, **경제지표 → 기업 실적 → 밸류에이션 → 뉴스**가 서로 연결된 분석용 데이터베이스가 되어 LLM이 "반도체 섹터가 현재 과대평가인지" 또는 "지금이 경기 후반부인지" 같은 질문에 훨씬 근거 있는 답변을 생성할 수 있습니다.
