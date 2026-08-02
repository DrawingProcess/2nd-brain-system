# Inbox 분류 테스트: 뉴스 기사 1건

**작성일**: 2026-07-31
**작성자**: Claude Code
**목적**: finance 도메인 스키마([[260731_02_finance-wiki-domain-setup]]) 적용 후,
실제 뉴스 기사 URL 1건으로 inbox → raw 분류 워크플로우를 검증

---

## 1. 입력

- URL: `https://finance.yahoo.com/markets/stocks/articles/korean-stocks-jump-record-14-000934073.html`
- 내용: Bloomberg 기사, "Korean Stocks Jump Record 14% on Renewed AI Trade Optimism"
  (Youkyung Lee, 2026-07-31 게재)

## 2. 처리 과정

1. **Fetch**: WebFetch로 기사 제목/본문/출처를 추출.
2. **검증**: Kospi +14%, SK Hynix +28%, Samsung +26%라는 수치가 역사상 최대급으로
   이례적이어서, WebFetch가 내부적으로 요약 모델을 거치는 점을 감안해 `curl`로 원본
   HTML을 직접 받아 제목 태그·`og:title`·본문 텍스트를 대조 확인함. 수치와 본문이
   실제 게재 기사와 정확히 일치함을 확인 (사실관계 자체가 아니라 "원문에 실제로
   이렇게 보도됐는지"를 확인한 것).
3. **Inbox 적재**: `inbox/korean-stocks-jump-record-14pct-ai-optimism.md`에 출처 URL과
   캡처 시각만 붙여 임시 적재.
4. **분류 결정**:
   - 디렉토리: `raw/articles/` (뉴스/기사 캡처)
   - 태그: `news`, `equity`, `macro` (finance 태그 taxonomy 활용)
   - Canonical 승격 여부: 보류 — 단일 소스이고, 반복 등장하는 두 번째 소스가 아직
     없어 SCHEMA.md의 승격 기준(2개 이상 소스에서 반복 또는 단일 소스의 중심 주제)을
     이번 단계에서는 충족시키지 않는 것으로 판단. 향후 SK Hynix, Samsung Electronics,
     Kospi 관련 소스가 추가되면 `entities/`(종목)와 `concepts/`(밸류에이션/시장 변동성
     등) 승격을 검토.
5. **Raw 레코드 생성**: `raw/articles/korean-stocks-jump-record-14pct-ai-optimism.md`에
   frontmatter(title, source, author, published, created, description, tags,
   sha256) + 본문 전문을 기록. `sha256`은 frontmatter 종료 `---` 다음 바이트부터
   파일 끝까지의 정확한 바이트에 대해 계산.
6. **정리**: 분류 완료 후 `inbox/`의 임시 파일 삭제 (inbox는 non-canonical 임시
   영역이므로).
7. **기록**: `log.md`에 `ingest` 액션 항목 추가.

## 3. 결과

| 항목 | 값 |
| --- | --- |
| 신규 raw 레코드 | `raw/articles/korean-stocks-jump-record-14pct-ai-optimism.md` |
| 분류 디렉토리 | `raw/articles/` |
| 태그 | `news`, `equity`, `macro` |
| Canonical 페이지 생성 | 0건 (보류) |
| `index.md` 변경 | 없음 |
| `log.md` | `ingest` 항목 1건 추가 |

## 4. 확인된 워크플로우

`inbox/` (임시 적재) → 분류 판단(디렉토리·태그·승격 여부) → `raw/<kind>/` (불변
레코드 + sha256) → `inbox/` 정리 → `log.md` 기록. Finance 도메인 스키마 확장
([[260731_02_finance-wiki-domain-setup]])이 실제 뉴스 기사 분류에 그대로
적용됨을 확인함.

## 5. 다음 단계

- SK Hynix, Samsung Electronics, Kospi 관련 두 번째 소스가 들어오면 `entities/`
  승격 여부 재검토.
- 공시(`raw/filings/`)나 실적발표(`raw/earnings/`) 유형 소스로 동일한 분류
  테스트를 확장.
