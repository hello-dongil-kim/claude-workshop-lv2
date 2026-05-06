---
name: session3-mcp-hooks
description: |
  MCP Servers & Hooks 실습. "MCP", "외부 도구 연결", "Hooks", "자동화", "세션 3", "Session 3" 키워드에 트리거.
  비개발자를 위한 MCP 서버 연결과 Hook 자동 품질 관리를 배우고 직접 설정한다.
---

# Session 3. MCP Servers & Hooks — 외부 도구 연결과 자동 품질 관리

> **난이도:** ★★★★☆ | **소요:** ~30분 | **블록:** 3개
> **대상:** Claude Code를 확장하려는 기획자, UX 리서처, PM
> **전제:** Session 1(CLAUDE.md), Session 2(Skills) 완료

## 용어 정리

| 용어 | 설명 |
|------|------|
| **MCP** | Model Context Protocol — Claude가 외부 서비스와 직접 소통하는 표준 규격 |
| **MCP Server** | MCP 규격으로 연결된 외부 서비스 (Notion, Slack, Gmail 등) |
| **Hook** | Claude 작업 흐름의 특정 시점에 자동 실행되는 쉘 스크립트 |
| **settings.json** | Claude Code의 설정 파일. MCP 서버와 Hook을 등록하는 곳 |

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
| 0 | MCP 개념 | MCP란? + 기획자용 서버 5개 + 연결 방법 | ~10분 |
| 1 | Hooks 개념 | Hooks란? + 4가지 시점 + 기획자 활용 예시 | ~10분 |
| 2 | 실습 | MCP 서버 1개 연결 + Hook 1개 설정 | ~10분 |

처음이면 Block 0부터 순서대로 진행을 추천한다.

---

## Block 0: MCP 개념

@references/block0-mcp.md 파일의 EXPLAIN → EXECUTE → QUIZ 순서로 진행.

## Block 1: Hooks 개념

@references/block1-hooks.md 파일의 EXPLAIN → EXECUTE → QUIZ 순서로 진행.

## Block 2: 실습

@references/block2-hands-on.md 파일의 EXPLAIN → EXECUTE → QUIZ 순서로 진행.

## 참고 템플릿

@templates/hook-template.md — Hook 설정 템플릿. 실습 시 참고용으로 안내할 수 있다.
