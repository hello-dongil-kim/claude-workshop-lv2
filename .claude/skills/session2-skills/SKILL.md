---
name: session2-skills
description: |
  Skills 작성 실습. "Skills", "스킬", "자동 트리거", "SKILL.md", "세션 2", "Session 2" 키워드에 트리거.
  비개발자를 위한 Skills 파일 구조와 작성법을 배우고 직접 만든다.
---

# Session 2. Skills — "맥락에 따라 자동 로딩되는 전문 지식"

> **난이도:** ★★★☆☆ | **소요:** ~35분 | **블록:** 3개
> **대상:** Claude Code를 처음 확장하는 기획자, UX 리서처, PM
> **전제:** Session 1(CLAUDE.md) 완료

## 용어 정리

| 용어 | 설명 |
|------|------|
| **Skill** | 대화 맥락에 따라 자동으로 로딩되는 전문 지식 파일 |
| **SKILL.md** | Skill의 핵심 파일. 역할, 원칙, 트리거 조건을 정의 |
| **description** | SKILL.md frontmatter의 필드. 자동 트리거 조건을 결정 |
| **references/** | Skill이 참조하는 보충 자료 폴더 |
| **examples/** | Skill이 참조하는 예시 폴더 |

---

## STOP PROTOCOL — 절대 위반 금지

각 블록은 반드시 **2턴**에 걸쳐 진행한다.

### Phase A (첫 번째 턴)
1. references 파일의 **EXPLAIN** 섹션을 읽고 설명
2. **EXECUTE** 섹션을 읽고 "직접 실행해보세요" 안내
3. **반드시 STOP** — 퀴즈 내지 않음, 도구 호출 금지

### Phase B (두 번째 턴)
1. **QUIZ** 섹션을 읽고 AskUserQuestion으로 퀴즈 출제
2. 정답/오답 피드백
3. 다음 블록 진행 여부 확인

### 절대 하지 않을 것
- Phase A에서 AskUserQuestion 호출
- Phase A에서 퀴즈 내기
- "실행해봤나요?" 질문
- 한 턴에 EXPLAIN + QUIZ

### Phase A 종료 시 필수 문구
```
---
위 내용을 직접 실행해보세요.
실행이 끝나면 "완료" 또는 "다음"이라고 입력해주세요.
```

---

## 시작

AskUserQuestion으로 시작 블록을 선택하게 한다:

| Block | 주제 | 내용 | 시간 |
|-------|------|------|------|
| 0 | 개념 | Skills란 무엇인가 + Commands와 차이 + 자동 트리거 | ~10분 |
| 1 | 구조 | SKILL.md 작성법 + description 트리거 설계 + 파일 구조 | ~12분 |
| 2 | 실습 | 나만의 첫 Skill 직접 만들기 | ~13분 |

처음이면 Block 0부터 순서대로 진행을 추천한다.

---

## Block 0: 개념

@references/block0-concept.md 파일의 EXPLAIN → EXECUTE → QUIZ 순서로 진행.

## Block 1: 구조

@references/block1-structure.md 파일의 EXPLAIN → EXECUTE → QUIZ 순서로 진행.

## Block 2: 실습

@references/block2-hands-on.md 파일의 EXPLAIN → EXECUTE → QUIZ 순서로 진행.
