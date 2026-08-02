# Finance 도메인 위키 확장 준비

**작성일**: 2026-07-31
**작성자**: Claude Code
**목적**: 기존 2nd-brain-system(PKM/AI 워크플로우 위키)에 financial 정보 수집·분류를
위한 finance 도메인을 추가하기 위한 스키마 확장 작업 기록

---

## 1. 배경

사용자는 financial 정보를 읽어서 자신만의 wiki를 구축하고 싶어했고, 분류를 체계적으로
해두고 싶다는 요구가 있었음. 별도 시스템을 새로 만들기보다, 기존 SCHEMA.md의 3계층
구조(raw → canonical → index/log)가 도메인에 무관하므로 그 위에 finance 도메인을
얹는 방식을 채택함.

## 2. 이번 작업 범위

이번 단계에서는 **분류 체계(스키마)만 확장**했고, 실제 raw 레코드나 canonical
페이지는 아직 생성하지 않음 (0건 유지). 실제 financial 원본 자료가 들어오는 다음
단계에서 아래 구조를 사용해 ingest/create를 진행하면 됨.

### 2.1 raw 소스 디렉토리 추가

| 경로 | 역할 |
| --- | --- |
| `raw/filings/` | 공시·규제 서류 (10-K, 10-Q, DART/SEC 공시 등) |
| `raw/earnings/` | 실적발표 컨퍼런스콜/브리핑 트랜스크립트 |

기존 `raw/articles/`(뉴스·기사), `raw/youtube/`(애널리스트 영상) 등은 그대로 재사용.

### 2.2 등록 태그 (SCHEMA.md 태그 taxonomy)

- `macro`: 거시경제 지표·정책·시장 전반 상황
- `equity`: 개별 종목·섹터·주식시장 분석
- `earnings`: 실적발표·기간별 실적 비교
- `filing`: 규제 공시·법정 서류
- `valuation`: 밸류에이션 방법론·재무 지표
- `crypto`: 디지털자산 시장·프로토콜
- `portfolio`: 포지션 사이징·자산배분·포트폴리오 전략

### 2.3 canonical 디렉토리 사용 지침 (스키마 변경 없음, 운용 가이드)

- `entities/`: 종목(ticker), 기업, 펀드, 매크로 지표 등 반복 등장하는 고유 개체
- `concepts/`: 밸류에이션 방법론, 재무비율, 투자 전략 등 이론/방법
- `comparisons/`: 종목 vs 종목, 전략 vs 전략 등 대조 분석
- `queries/`: "이번 분기 반도체 섹터 실적 종합" 같은 주기적 리서치 질의

## 3. 변경 파일

- `SCHEMA.md`: 디렉토리 역할 표에 `raw/filings/`, `raw/earnings/` 추가; 태그
  taxonomy에 finance 태그 7종 추가
- `raw/filings/.gitkeep`, `raw/earnings/.gitkeep`: 신규 디렉토리 플레이스홀더
- `log.md`: `[2026-07-31] update | finance 도메인 스키마 확장` 항목 추가
- `index.md`: 변경 없음 (canonical 페이지 0건 유지)

## 4. Ollama 우선 활용 전략 (권장, 미구현)

API 비용을 줄이면서 성능을 유지하기 위한 파이프라인 역할 분담:

- **로컬 모델(qwen3.5, gemma4) + Hermes Agent**: raw 원본 요약, 엔티티/태그 후보
  추출, frontmatter 초안 작성 등 반복적인 1차 컴파일 작업
- **Claude Code**: SCHEMA.md 준수 검증, wikilink 연결성(최소 2개) 판단,
  confidence/contested 같은 애매한 판단이 필요한 최종 승격(promotion) 게이트

로컬 모델 산출물은 canonical로 바로 승격하지 않고, 위 게이트를 통과한 후에만
`entities/`, `concepts/`, `comparisons/`, `queries/`에 반영하는 것을 권장.

## 5. 다음 단계

1. 실제 financial 원본(뉴스, 공시, 실적발표 등) 1건을 `inbox/`에 두고 분류 테스트
2. 분류 결과에 따라 `raw/filings/` 또는 `raw/earnings/`로 ingest
3. 두 번째 소스가 모일 때까지 canonical 페이지 생성을 보류 (SCHEMA.md 승격 기준:
   같은 주제가 최소 2개 소스에 등장하거나 단일 소스의 중심 주제일 때)
4. Hermes Agent(Understand-Anything)로 초안 생성 → Claude Code로 스키마 검증 후 확정
