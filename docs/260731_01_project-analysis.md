# 프로젝트 분석: 2nd-Brain-System

**작성일**: 2026-07-31
**작성자**: Claude Code Analysis
**목적**: CLAUDE.md 가이드라인 분석 및 2nd-brain-system 프로젝트 구조 이해

---

## 1. CLAUDE.md 가이드라인 분석

### 1.1 핵심 원칙

CLAUDE.md는 LLM 코딩 실수를 줄이기 위한 4가지 핵심 원칙을 정의합니다:

#### 1) Think Before Coding (사고 우선)
- 가정을 명시적으로 표현
- 여러 해석이 가능할 경우 모두 제시
- 불분명한 점은 즉시 질문
- 더 간단한 접근법이 있으면 제안

#### 2) Simplicity First (단순성 우선)
- 요청된 것만 구현, 추측성 기능 금지
- 단일 사용 코드에 대한 추상화 금지
- 불가능한 시나리오에 대한 에러 처리 금지
- 200줄로 작성했지만 50줄로 가능하면 재작성

#### 3) Surgical Changes (수술적 변경)
- 필요한 부분만 수정
- 인접 코드 개선 금지
- 기존 스타일 유지
- 자신의 변경으로 생긴 고아 코드만 제거

#### 4) Goal-Driven Execution (목표 지향 실행)
- 검증 가능한 성공 기준 정의
- 작업을 검증 가능한 목표로 변환
- 완료까지 독립적으로 루프

### 1.2 프로젝트 구조 정의

CLAUDE.md가 정의한 표준 구조:
```
./docs      - 실행 완료 후 요약 (YYMMDD_NN_description.md)
./scripts   - 셸 스크립트
./test      - 테스트 코드
./src       - Python 코드
```

---

## 2. 2nd-Brain-System 프로젝트 분석

### 2.1 프로젝트 정체성

**핵심 특징**:
- Markdown 기반 증거 중심 개인 지식 관리(PKM) 시스템
- Obsidian과 함께 사용하는 LLM Wiki 템플릿
- 데이터베이스나 빌드 시스템 없이 순수 Markdown + Git 관리
- 한국어 중심 문서화

**프로젝트 타입**: 문서 시스템 (코드 없음)

### 2.2 현재 상태 (2026-07-21 log 기준)

**파일 통계**:
- Raw source: 13개 (YouTube 3, NotebookLM 8, Web 2)
- Canonical 페이지: 8개 (Concepts 5, Comparisons 1, Queries 2)
- Entities: 0개
- 등록된 태그: 9개
- Canonical 링크: 33개

**무결성 상태**:
- 기록된 SHA-256 해시: 8개 매칭
- Legacy 파일 (해시 없음): 5개 (문서화된 갭)
- Lint 오류: 0

### 2.3 실제 디렉토리 구조

```
/SSD1/sjchoi/2nd-brain-system/
├── inbox/              # 임시 입력 대기 (분류 전)
├── raw/                # Layer 1: 불변 원본 증거
│   ├── articles/       # 기사 및 웹 클리핑
│   ├── notebooklm/     # NotebookLM 소스 레코드 (8개)
│   ├── transcripts/    # 오디오/비디오 트랜스크립트
│   ├── web/            # 웹 캡처 (2개)
│   ├── youtube/        # YouTube 메타데이터/트랜스크립트 (3개)
│   └── assets/         # 이미지 및 첨부파일
├── entities/           # Layer 2: 개체 정의 (현재 0개)
├── concepts/           # Layer 2: 개념 정의 (5개)
├── comparisons/        # Layer 2: 비교 분석 (1개)
├── queries/            # Layer 2: 질의와 합성 답변 (2개)
├── docs/               # 아키텍처/워크플로우 문서
│   ├── architecture/   # 아키텍처 다이어그램
│   ├── tech-stack/     # 기술 스택 다이어그램
│   └── workflow/       # 워크플로우 다이어그램
├── .obsidian/          # Obsidian 공유 설정
├── SCHEMA.md           # Layer 3: 권위 데이터 계약
├── AGENTS.md           # 프로젝트 지식베이스 (에이전트용)
├── README.md           # 사용 가이드 (영문)
├── README.ko.md        # 사용 가이드 (한글)
├── index.md            # Layer 3: 활성 canonical 페이지 카탈로그
└── log.md              # Layer 3: Append-only 작업 이력
```

**누락된 디렉토리** (CLAUDE.md 기준):
- `scripts/` - 존재하지 않음
- `src/` - 존재하지 않음
- `test/` - 존재하지 않음

**선택적 디렉토리** (필요시 생성):
- `raw/papers/files/` - 논문 첨부파일 복사본
- `templates/` - 검증된 노트 템플릿
- `_archive/` - 완전히 대체된 canonical 지식

---

## 3. 핵심 아키텍처

### 3.1 3계층 구조

#### Layer 1: Raw Immutable Source Evidence
- 위치: `raw/` 하위 디렉토리
- 특성: 캡처 후 불변 (immutable)
- 무결성: SHA-256 해시로 검증
- 허용된 변경:
  - Zotero 메타데이터 수리 (본문 보존)
  - NotebookLM frontmatter 매핑 (본문 보존)

#### Layer 2: Canonical Knowledge
- 위치: `entities/`, `concepts/`, `comparisons/`, `queries/`
- 특성: 검증된 재사용 가능 지식
- 요구사항:
  - 필수 frontmatter 필드 (title, created, updated, type, tags, sources, confidence, contested, contradictions)
  - 디렉토리와 type 일치
  - 최소 2개 다른 페이지와 wikilink 연결
  - 실존하는 raw/*.md 경로만 sources에 포함

#### Layer 3: Schema, Navigation, Log Metadata
- `SCHEMA.md`: 권위 계약 정의
- `index.md`: 완전한 활성 canonical 카탈로그
- `log.md`: Append-only 작업 이력

### 3.2 운영 워크플로우

```
Capture → Compile → Discovery → Human Decision
   ↓         ↓          ↓            ↓
 Inbox    Raw/*    NotebookLM    Verification
           ↓       UA Graph          ↓
      Integrity  → Discovery → Canonical Pages
       Check      Candidates     ↓
                               index.md
                               log.md
```

**검증 게이트**:
1. Integrity check (무결성)
2. Frontmatter validation (메타데이터)
3. Structural validation (구조)
4. Human approval (인간 승인)

**동기화 규칙**:
- Canonical 페이지 생성/수정/삭제 시 index.md + log.md 동시 업데이트
- log.md는 append-only (재작성/삭제 금지)

---

## 4. 기술 스택

### 4.1 핵심 자산 (Durable Assets)
- Open-format source material (Markdown, PDF)
- Canonical Markdown
- Provenance metadata
- Git history

### 4.2 도구 (Replaceable Tools)

#### 필수
- **Obsidian**: Markdown 편집 및 wikilink 탐색

#### 데이터 캡처
- **Zotero + Zotero Connector**: 논문 관리 및 웹 메타데이터 저장
- **Obsidian Web Clipper**: 웹 페이지 → Markdown 변환

#### AI 자동화 (MCP/CLI/Skills)
- **Zotero MCP**: 에이전트가 Zotero 데이터 접근
- **llm-wiki skill**: 소스 자료 → canonical 지식 컴파일
- **notebooklm-py**: NotebookLM 노트북 관리 및 질의 자동화
- **Understand Anything**: 지식 그래프 생성 및 관계 분석

### 4.3 검증 메커니즘
- UTF-8, LF line endings, no BOM
- Frontmatter 필수 필드 검증
- 등록된 태그만 사용
- Source 경로 실존 검증
- Wikilink 연결성 검증 (최소 2개)
- SHA-256 해시 매칭

---

## 5. 데이터 관리 원칙

### 5.1 불변성 (Immutability)
- Raw 파일 본문은 캡처 후 불변
- 수정은 canonical 페이지에만 허용
- 예외: 명시적으로 허용된 메타데이터 수리 작업만

### 5.2 Source Provenance
- 모든 canonical sources는 실존하는 `raw/*.md` 파일
- PDF/이미지 첨부파일만으로는 유효한 source 아님
- Claim-level 마커: `^[raw/...md]` 형식

### 5.3 연결성 (Connectivity)
- Canonical 페이지 ≥ 2개일 때, 모든 페이지는 최소 2개 다른 페이지와 연결
- 1-2개 페이지 canonical set은 무효
- Template, raw, archive, 같은 페이지 링크는 카운트 제외

### 5.4 선택적 승격 (Selective Promotion)
- 중심 주제이거나 2개 이상 소스에서 반복될 때만 canonical 페이지 생성
- 기존 주제가 있으면 새 증거를 추가 (중복 페이지 생성 금지)

### 5.5 변경 기록 (Change Recording)
- 모든 canonical 작업은 index.md + log.md 동시 업데이트
- log.md 항목 형식: `## [YYYY-MM-DD] <action> | <subject>`
- 허용된 action: ingest, create, update, query, lint, archive, delete, map, repair

---

## 6. 주요 발견사항

### 6.1 CLAUDE.md와의 불일치

**CLAUDE.md 기대**:
```
./docs      - 요약 문서
./scripts   - 셸 스크립트
./test      - 테스트 코드
./src       - Python 코드
```

**2nd-brain-system 실제**:
```
./docs      - 아키텍처/워크플로우 다이어그램
./scripts   - 존재하지 않음
./test      - 존재하지 않음
./src       - 존재하지 않음
```

**결론**: 2nd-brain-system은 순수 문서 관리 시스템으로, CLAUDE.md의 코드 프로젝트 구조와 다릅니다. SCHEMA.md가 실제 권위 계약입니다.

### 6.2 프로젝트 성격

- **타입**: 지식 관리 템플릿 (코드 없음)
- **타겟 사용자**: 연구자, 지식 노동자
- **주요 언어**: 한국어 (일부 영문)
- **주요 형식**: Markdown (UTF-8, LF)
- **버전 관리**: Git

### 6.3 현재 사용 중인 도구

**확인된 도구**:
- Obsidian (`.obsidian/` 설정 존재)
- Git (`.git/` 존재)
- YouTube 캡처 (3개 파일)
- NotebookLM (8개 파일)
- Web Clipper (2개 파일)

**아직 사용하지 않은 도구**:
- Zotero (raw/papers/ 디렉토리 비어 있음)
- Understand Anything (`.ua/` 디렉토리 없음)
- Python 스크립트
- 자동화 스크립트

### 6.4 지식베이스 현황

**Canonical 페이지 주제** (8개):

**Concepts (5)**:
1. ai-knowledge-workflow - 수집→검증→산출 워크플로우
2. ai-personal-knowledge-management - 3계층 PKM 원칙
3. llm-wiki - 지속형 Markdown 지식베이스
4. research-feedback-loop - 검증 및 환류 순환
5. second-brain-research-workflow - 증거 기반 연구 환경

**Comparisons (1)**:
1. knowledge-tool-roles - Zotero/NotebookLM/LLM Wiki/Obsidian 책임 비교

**Queries (2)**:
1. notebooklm-query-compounding - NotebookLM 질의 증분 편입
2. ua-knowledge-graph-workflow - 지식그래프 생성/분석/갱신

**태그 분포** (9개 등록):
- automation, comparison, knowledge-base, knowledge-graph
- notebooklm, pkm, provenance, research, workflow

### 6.5 품질 지표

**무결성**:
- ✅ 13/13 파일 byte-identical 복사
- ✅ 8/8 기록된 해시 매칭
- ⚠️ 5개 legacy 파일 해시 미기록 (문서화된 갭)

**연결성**:
- ✅ 33개 canonical wikilink
- ✅ 최소 페이지당 3개 outbound link
- ✅ 최소 페이지당 2개 inbound link
- ✅ 고아 페이지 없음

**Provenance**:
- ✅ 30개 source 참조 (실존 경로)
- ✅ 17개 claim-level 마커 (실존 경로)
- ✅ Broken link 없음

---

## 7. 다음 단계 권장사항

### 7.1 CLAUDE.md 가이드라인 준수

이 프로젝트에서 향후 작업 시:

1. **사고 우선**:
   - Canonical 페이지 생성 전 중복 여부 확인 (index.md 확인)
   - 불분명한 주제 분류는 질문

2. **단순성 우선**:
   - 요청된 주제만 문서화
   - 과도한 메타데이터 추가 금지

3. **수술적 변경**:
   - 관련 파일만 수정
   - index.md + log.md 동시 업데이트

4. **목표 지향**:
   - 검증 가능한 기준: lint 0 error, wikilink ≥2, sources 실존

### 7.2 프로젝트 확장 시 고려사항

**코드 추가 시**:
- CLAUDE.md 규칙에 따라 `scripts/`, `src/`, `test/` 생성
- SCHEMA.md에 새 디렉토리 역할 등록
- docs/에 실행 요약 작성 (YYMMDD_NN_description.md)

**지식베이스 확장 시**:
- 50개 항목마다 index.md 섹션 분할
- 200개 항목에서 주제별 네비게이션 맵 추가
- 500개 log 항목에서 log 순환 (log-YYYY.md)

**도구 추가 시**:
- SCHEMA.md에 태그 먼저 등록
- README.md 설치 가이드 업데이트
- AGENTS.md에 도구 역할 문서화

---

## 8. 결론

2nd-brain-system은 증거 기반 지식 관리의 우수 사례를 보여주는 잘 구조화된 Markdown 시스템입니다. CLAUDE.md가 정의한 코드 프로젝트 구조와는 다르지만, 그 핵심 원칙(사고 우선, 단순성, 수술적 변경, 목표 지향)은 지식 큐레이션 작업에도 완벽히 적용됩니다.

현재 시스템은 순수 문서 기반이며 코드가 없지만, 명확한 계약(SCHEMA.md), 완전한 추적성(log.md), 강력한 무결성 검증을 통해 신뢰할 수 있는 지식 자산을 구축하고 있습니다.
