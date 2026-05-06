# Block 1: Subagent 설계

## EXPLAIN

### 기획자용 Subagent 설계하기

Subagent는 `.claude/agents/` 폴더에 SKILL.md 파일로 정의한다. 일반 Skill(`.claude/skills/`)과 달리 **독립 폴더에 위치**하며, **에이전트 전용 frontmatter 필드**를 추가하면 Subagent로 동작한다.

### desk-researcher 에이전트 설계 예시

아래는 기획자가 리서치 작업을 위임할 수 있는 `desk-researcher` 에이전트의 전체 SKILL.md다:

```markdown
---
name: desk-researcher
description: |
  데스크 리서치 전문 에이전트.
  "리서치해줘", "조사해줘", "시장 분석", "경쟁사 분석" 키워드에 트리거.
  주어진 주제를 조사하고 구조화된 요약본을 반환한다.
model: sonnet
maxTurns: 15
tools:
  - WebSearch
  - Read
  - Write
---

# Desk Researcher

## 역할
너는 기획자를 보조하는 데스크 리서치 전문가다.
주어진 주제에 대해 빠르게 조사하고, 구조화된 요약본을 작성한다.

## 작업 원칙
- 사실(Fact)과 의견(Opinion)을 명확히 구분
- 출처를 반드시 표기 (URL 또는 문서명)
- 핵심 발견 3~5개를 먼저 제시하고, 상세 내용은 뒤에 배치
- 리서치 범위와 한계를 명시

## 산출물 형식
조사 결과는 아래 구조로 작성:

### [주제명] 리서치 요약
- **핵심 발견**: 3~5개 불릿
- **상세 분석**: 발견별 근거와 데이터
- **출처 목록**: 참고한 자료 리스트
- **리서치 한계**: 이번 조사에서 다루지 못한 부분
```

### frontmatter 필드 설명

| 필드 | 값 | 설명 |
|------|-----|------|
| `name` | `desk-researcher` | 에이전트 호출명. `@desk-researcher`로 호출 |
| `description` | 트리거 키워드 포함 | 언제 이 에이전트가 활성화되는지 기술 |
| `model` | `sonnet` | 사용할 모델. 보조 작업은 sonnet으로 비용 절약 |
| `maxTurns` | `15` | 에이전트가 자율적으로 수행할 수 있는 최대 턴 수 |
| `tools` | `WebSearch`, `Read`, `Write` | 에이전트가 사용할 수 있는 도구 목록 |

### model 필드 선택 기준

| 모델 | 용도 | 비용 |
|------|------|------|
| `opus` | 복잡한 판단, 전략 수립, 고품질 문서 작성 | 높음 |
| `sonnet` | 리서치, 요약, 데이터 정리, 일반 보조 작업 | 중간 |
| `haiku` | 단순 반복 작업, 포맷 변환, 분류 | 낮음 |

**원칙:** Subagent는 메인 Claude의 보조 역할이므로, 대부분 `sonnet`이면 충분하다. 비용 대비 품질이 가장 균형 잡힌 선택이다.

### 설계 시 고려사항 3가지

| 항목 | 질문 | 예시 |
|------|------|------|
| **역할** | 이 에이전트는 무엇을 전문으로 하는가? | 데스크 리서치, 회의록 정리, 데이터 분석 |
| **원칙** | 작업 시 반드시 지켜야 할 규칙은? | 출처 표기, 사실/의견 구분, 한국어 작성 |
| **산출물 형식** | 결과를 어떤 구조로 받고 싶은가? | 핵심 발견 → 상세 분석 → 출처 → 한계 |

### 기획자가 만들 수 있는 Subagent 예시

| 에이전트명 | 역할 | 주요 도구 |
|------------|------|-----------|
| `desk-researcher` | 시장/경쟁사/트렌드 리서치 | WebSearch, Read, Write |
| `meeting-scribe` | 회의록 정리 및 액션 아이템 추출 | Read, Write |
| `data-formatter` | 데이터 정리, 포맷 변환, 테이블 구조화 | Read, Write |
| `ux-reviewer` | 사용성 체크리스트 기반 리뷰 | Read, Write |

### 자주 발생하는 문제와 해결법

| 증상 | 원인 | 해결 |
| ---- | ---- | ---- |
| `/agents`에 에이전트가 안 보임 | SKILL.md 위치 오류 | `.claude/agents/{에이전트명}/SKILL.md` 경로 확인 |
| `@에이전트명`으로 호출이 안 됨 | name 필드 불일치 | SKILL.md frontmatter의 `name`과 호출명이 같은지 확인 |
| 에이전트가 도구를 사용하지 못함 | tools 목록 누락 | frontmatter의 `tools:` 에 필요한 도구 추가 (WebSearch, Read 등) |
| 결과 품질이 기대 이하 | model 또는 maxTurns 부족 | 복잡한 분석은 `model: opus`, 탐색 작업은 `maxTurns: 20` 이상 |

**안 되면 이것부터 확인 — 디버깅 3단계:**

```text
1단계: Claude에게 물어보기
  "방금 만든 에이전트가 /agents에 안 보여.
   SKILL.md를 확인하고 문제를 찾아줘."
  → 경로 오류, name 불일치 등 대부분 여기서 해결

2단계: 에이전트 재생성 요청
  "이 에이전트의 SKILL.md를 다시 만들어줘.
   name은 {이름}, 역할은 {역할}로."
  → YAML 구문 오류 등 꼬인 설정 해결

3단계: 설정 비교 요청
  "내 에이전트 SKILL.md와 @templates/subagent-template.md를
   비교해서 빠진 부분을 알려줘."
  → 템플릿과의 차이에서 원인 발견
```

> **핵심: 에러 메시지를 이해할 필요 없다. Claude에게 "안 돼, 고쳐줘"라고 말하면 된다.**

---

## EXECUTE

다음을 직접 실행해보세요:

**Step 1: Claude에게 Subagent 만들어달라고 요청**

```text
내 업무에서 반복되는 보조 작업을 자동화할 Subagent를 만들어줘.
@templates/subagent-template.md 를 참고해서.
역할: {예: 데스크 리서처, 회의록 정리, 경쟁사 모니터링 등}
이 에이전트가 할 일: {구체적 작업 설명}
.claude/agents/{에이전트명}/SKILL.md 로 생성해줘.
```

- Claude가 생성한 SKILL.md를 검토
- model, maxTurns, tools 설정이 적절한지 확인
- **핵심: YAML 문법을 몰라도 된다. Claude에게 시키고 결과를 검토하면 된다**

**Step 2: 테스트**

```text
/agents
```

- 새로 만든 에이전트가 목록에 나타나는지 확인
- `@에이전트명 [작업 지시]`로 호출하여 결과를 확인
- 결과가 기대와 다르면: "역할 설명을 이렇게 바꿔줘", "tools에 WebSearch도 추가해줘" 등 수정 지시

---

## QUIZ

**문제:** Subagent의 model 필드를 `sonnet`으로 설정하는 가장 적절한 이유는?

| 선택지 | 내용 |
|--------|------|
| A | 보조 작업에는 비용 대비 품질이 균형 잡힌 모델이 적합하므로 |
| B | sonnet이 Subagent 전용으로 최적화된 모델이라서 |
| C | opus보다 응답 속도가 빨라 리서치에 유리하므로 |

**정답:** A — Subagent는 메인 Claude의 보조 역할이므로, 대부분의 리서치/요약/정리 작업에는 sonnet의 성능이면 충분하다. opus도 사용 가능하지만 비용이 높아, 복잡한 판단이 필요한 경우에만 선택한다.
