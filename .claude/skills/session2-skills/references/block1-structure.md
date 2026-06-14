# Block 1: Skills 파일 구조

## EXPLAIN

### Skill 폴더 구조

하나의 Skill은 다음과 같은 폴더 구조를 가진다:

```
.claude/skills/ux-research/
├── SKILL.md            ← 핵심 파일 (역할, 원칙, 트리거 조건)
├── references/         ← 보충 자료 (프레임워크, 가이드라인)
│   ├── interview-guide.md
│   └── usability-test-checklist.md
└── examples/           ← 예시 (실제 산출물 샘플)
    ├── interview-script-sample.md
    └── test-report-sample.md
```

| 구성 요소 | 역할 | 필수 여부 |
|-----------|------|-----------|
| `SKILL.md` | Skill의 정체성 — 이름, 트리거 조건, 역할, 원칙 | **필수** |
| `references/` | Skill이 참조하는 지식 — 프레임워크, 체크리스트, 가이드라인 | 선택 |
| `examples/` | 산출물 예시 — Claude가 형식과 톤을 참고 | 선택 |

### SKILL.md 작성법

SKILL.md는 두 부분으로 구성된다:

**1. Frontmatter (YAML)**
```yaml
---
name: ux-research
description: |
  인터뷰, 사용성 테스트, 설문, FGI, 리서치 설계, 리서치 플랜 키워드 시 트리거.
  UX 리서처가 리서치를 설계하고 실행할 때 전문 지식을 제공한다.
---
```

| 필드 | 역할 | 예시 |
|------|------|------|
| `name` | Skill 식별자 (폴더명과 일치 권장) | `ux-research` |
| `description` | **자동 트리거 조건** + Skill 요약 | 아래 상세 설명 |

**2. 본문 (Markdown)**
```markdown
# UX Research Skill

## 역할
너는 UX 리서치 전문가다. 사용자의 리서치 설계, 실행, 분석을 돕는다.

## 원칙
- 리서치 목적을 먼저 확인하고 방법론을 추천
- 정성/정량 리서치를 균형 있게 제안
- 결과 해석 시 편향(bias) 가능성을 항상 언급

## 참조
- @references/interview-guide.md — 인터뷰 가이드
- @references/usability-test-checklist.md — 사용성 테스트 체크리스트
```

### description 필드 — "요약"이 아니라 "트리거 조건"

description은 Skill의 설명이 아니다. **Claude가 이 Skill을 언제 로딩할지 판단하는 기준**이다.

이것이 Skills에서 가장 중요한 설계 포인트다:

| 구분 | description | 왜 문제인가 / 왜 좋은가 |
|------|-------------|-------------------------|
| **나쁜 예** | "UX 리서치를 도와줍니다" | 너무 추상적. "도와줍니다"는 트리거 키워드가 아님 |
| **나쁜 예** | "리서치 Skill입니다" | 자기 설명일 뿐, 매칭 조건이 없음 |
| **좋은 예** | "인터뷰, 사용성 테스트, 설문, FGI, 리서치 설계 키워드 시 트리거" | 구체적 키워드 나열 → 매칭 정확도 상승 |
| **좋은 예** | "PRD, 화면 설계, 정책 정의, 기능 명세, 사용자 스토리 키워드 시 트리거" | 기획 도메인의 구체적 작업 나열 |

### 좋은 description 작성 공식

```
[구체적 키워드 나열] + 키워드 시 트리거.
[Skill이 하는 일 한 줄 요약].
```

예시:
```yaml
description: |
  워크숍, 퍼실리테이션, 아이데이션, 브레인스토밍, 디자인 스프린트 키워드 시 트리거.
  워크숍과 협업 세션을 설계하고 퍼실리테이션 가이드를 제공한다.
```

### 참조 파일 연결 방법

SKILL.md 본문에서 `@references/파일명.md` 또는 `@examples/파일명.md`로 연결한다:

```markdown
## 참조
- @references/interview-guide.md — 심층 인터뷰 질문 구성 가이드
- @examples/interview-script-sample.md — 실제 인터뷰 스크립트 예시
```

Claude는 이 참조 파일들을 함께 읽고, 더 전문적이고 일관된 산출물을 만든다.

### 고급 frontmatter 필드 (참고)

기본 `name`과 `description` 외에, 기획자에게 유용한 고급 필드가 있다:

| 필드 | 역할 | 기획자 활용 예시 |
|------|------|------------------|
| `disable-model-invocation: true` | Claude가 자동 로딩하지 않음. `/명령어`로만 호출 | 배포, 보고서 전송 등 부작용 있는 작업 |
| `paths` | 특정 파일 유형에서만 트리거 | `"**/*.md"` → 마크다운 작업 시에만 활성화 |
| `allowed-tools` | Skill 활성화 시 사용 가능한 도구 제한 | `Read Grep Glob` → 읽기 전용 리서치 모드 |
| `context: fork` | 별도 독립 공간에서 실행 (메인 대화와 분리) | 리서치 작업을 독립 컨텍스트에서 실행 |

> 지금 전부 외울 필요 없다. 필요할 때 Claude에게 "이 Skill을 수동 호출 전용으로 바꿔줘"라고 말하면 된다.

---

## EXECUTE

다음을 직접 실행해보세요:

**Step 1: 기존 스킬의 SKILL.md 분석**
```
.claude/skills/ 폴더에 있는 스킬 중 하나의 SKILL.md를 읽어줘.
frontmatter의 name과 description을 분석해서 보여줘.
```

**Step 2: description 품질 평가**
- 읽은 SKILL.md의 description이 "트리거 조건"으로서 충분한지 평가해보세요
- 구체적 키워드가 나열되어 있는지, 아니면 추상적 설명인지 확인
- 개선한다면 어떻게 쓸지 생각해보세요

> ✅ **이렇게 되면 성공:** 읽은 SKILL.md의 description이 "구체적 키워드 나열"인지 "추상적 설명"인지 판단하고, 추상적이라면 더 나은 키워드 버전을 한 줄로 제시할 수 있으면 성공.

---

## QUIZ

**문제 1 (회상형):** SKILL.md의 description 필드의 핵심 역할은?

| 선택지 | 내용 |
|--------|------|
| A | Claude가 Skill을 자동 로딩할지 판단하는 트리거 조건 |
| B | Skill의 기능을 사용자에게 설명하는 문서 |
| C | Skill의 버전과 작성자를 기록하는 메타데이터 |

**정답:** A — description은 사용자를 위한 설명이 아니라, Claude가 대화 맥락과 매칭하여 Skill을 자동 로딩할지 결정하는 트리거 조건이다. 구체적 키워드를 나열해야 매칭 정확도가 올라간다.
- B 오답: 사용자 설명문처럼 쓰면("도와줍니다") 매칭할 키워드가 없어 트리거가 안 된다.
- C 오답: 버전·작성자 기록 용도가 아니다 — description은 순수하게 트리거 판단용이다.

**문제 2 (적용형):** 다음 상황에서 가장 적절한 것은? — 인터뷰 정리 Skill을 만들었는데, "인터뷰 정리해줘"라고 해도 자동으로 안 켜진다. description에는 "리서치를 도와줍니다"라고만 적혀 있다.

| 선택지 | 내용 |
|--------|------|
| A | SKILL.md 본문(역할·원칙)을 더 길게 보강한다 |
| B | description을 "인터뷰, FGI, 사용자 인터뷰, 인터뷰 정리, 녹취록 키워드 시 트리거"처럼 구체적 키워드로 바꾼다 |
| C | 매번 `/스킬명`으로 수동 호출하기로 한다 |

**정답:** B — 자동 트리거는 description의 키워드 매칭으로 결정된다. 실제 쓸 표현을 키워드로 나열해야 켜진다.
- A 오답: 본문을 늘려도 트리거 판단에는 영향이 없다 — 켜진 뒤 품질만 달라진다.
- C 오답: 작동은 하지만 "자동 로딩"이라는 Skill의 핵심 이점을 포기하는 우회책이다.
