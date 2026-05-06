---
name: session1-claude-md
description: |
  CLAUDE.md 작성 실습. "CLAUDE.md", "프로젝트 브리핑", "컨텍스트 설정", "세션 1", "Session 1" 키워드에 트리거.
  비개발자를 위한 CLAUDE.md 작성법을 배우고 직접 만든다.
---

# Session 1. CLAUDE.md — 프로젝트의 "컨텍스트 브리핑"

> **난이도:** ★☆☆☆☆ | **소요:** ~46분 | **블록:** 4개
> **대상:** Claude Code를 처음 확장하는 기획자, UX 리서처, PM
> **전제:** Claude Code 설치 완료, 터미널에서 기본 대화 경험 있음

## 용어 정리

| 용어 | 설명 |
|------|------|
| **CLAUDE.md** | 매 세션 시작 시 자동으로 읽히는 프로젝트 설정 문서 |
| **컨텍스트** | Claude가 작업할 때 참조하는 배경 정보 |
| **컨텍스트 윈도우** | Claude가 한 세션에서 기억할 수 있는 총 용량 |

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
| 0 | 개념 | CLAUDE.md + 권한 모드 4종 + 컨텍스트 관리 | ~12분 |
| 1 | 실습 | /init → 커스텀 + 4단계 워크플로우 체험 | ~14분 |
| 2 | 심화 | 프롬프트 패턴 + 메모리 + 비용 관리 + 팀 공유 | ~10분 |
| 3 | 구조 | 프로젝트 전체 맵 — .claude/ 폴더와 확장 구조 | ~10분 |

처음이면 Block 0부터 순서대로 진행을 추천한다.

---

## Block 0: 개념

@references/block0-concept.md 파일의 EXPLAIN → EXECUTE → QUIZ 순서로 진행.

## Block 1: 실습

@references/block1-hands-on.md 파일의 EXPLAIN → EXECUTE → QUIZ 순서로 진행.

## Block 2: 심화

@references/block2-advanced.md 파일의 EXPLAIN → EXECUTE → QUIZ 순서로 진행.

## Block 3: 프로젝트 구조

@references/block3-project-structure.md 파일의 EXPLAIN → EXECUTE → QUIZ 순서로 진행.
