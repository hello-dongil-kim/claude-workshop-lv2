---
name: workshop-plugins
description: |
  Plugins 워크숍. "Plugin", "플러그인", "배포", "팀 표준", "Workshop", "워크숍" 키워드에 트리거.
  Session 1~4에서 배운 모든 확장 기능을 패키지로 묶어 배포하는 방법을 실습한다.
---

# Workshop. Plugins — 확장 기능을 패키지로 묶어 배포하기

> **난이도:** ★★★★★ (실습) | **소요:** ~25분 | **블록:** 2개
> **대상:** Claude Code를 확장하려는 기획자, UX 리서처, PM
> **전제:** Session 1~4 이해 (CLAUDE.md, Skills, MCP/Hooks, Subagents/Agent Teams)

## 용어 정리

| 용어 | 설명 |
|------|------|
| **Plugin** | Skills + Commands + Subagents를 하나의 패키지로 묶어 설치/공유하는 단위 |
| **Marketplace** | 플러그인을 검색/설치할 수 있는 저장소 (GitHub 레포 등) |
| **네임스페이스** | `플러그인명:스킬명` 형식으로 충돌을 방지하는 명명 규칙 |

---

## 진도 관리 — 시작 시 먼저 확인

세션을 시작하면 **블록 선택 전에** 아래를 처리한다:

1. **이어하기 확인** — 프로젝트 루트에 `progress.md`가 있으면 읽고, 완료된 WS 블록을 보여준 뒤 "이어서 다음 블록부터 진행할까요?"라고 제안한다. 없으면 그냥 Block 0부터 안내한다.
2. **블록 완료 시 기록** — 각 블록의 Phase B(퀴즈 피드백)가 끝나면 `progress.md`의 해당 줄을 `[x]`로 갱신한다. (파일이 없으면 README의 체크리스트를 복사해 새로 만들어도 좋은지 사용자에게 확인)
3. **적응형 건너뛰기** — 사용자가 "이 블록 알아요" / "건너뛸래요"라고 하면, 해당 블록 EXPLAIN을 **1분 요약**으로 압축해 전달한 뒤 바로 Phase B(퀴즈)로 넘어간다. 퀴즈를 맞히면 완료 처리, 틀리면 아래 remediation을 따른다.

---

## STOP PROTOCOL — 절대 위반 금지

각 블록은 반드시 **2턴**에 걸쳐 진행한다.

### Phase A (첫 번째 턴)
1. references 파일의 **EXPLAIN** 섹션을 읽고 설명
2. **EXECUTE** 섹션을 읽고 "직접 실행해보세요" 안내
3. **반드시 STOP** — 퀴즈 내지 않음, 도구 호출 금지

### Phase B (두 번째 턴)
1. **QUIZ** 섹션을 읽고 AskUserQuestion으로 퀴즈 출제 (회상형 + 적용형 2문항)
2. 정답/오답 피드백
3. **오답 시 remediation** — 틀린 문항과 연결된 EXPLAIN 구간을 다시 짚어 1~2문장으로 설명하고, 같은 문항을 한 번 더 풀게 한다. 두 번째도 틀리면 정답·근거를 알려주고 다음으로 넘어간다.
4. `progress.md` 해당 블록을 `[x]`로 갱신
5. 다음 블록 진행 여부 확인

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
| 0 | 개념 + 탐색 | Plugin이란? + 비유 + 설치/탐색 방법 | ~10분 |
| 1 | 실습 | 플러그인 설치 체험 + 나만의 Skill 만들기 | ~15분 |

처음이면 Block 0부터 순서대로 진행을 추천한다.

---

## Block 0: 개념 + 탐색

@references/block0-concept.md 파일의 EXPLAIN → EXECUTE → QUIZ 순서로 진행.

## Block 1: 실습

@references/block1-hands-on.md 파일의 EXPLAIN → EXECUTE → QUIZ 순서로 진행.

## 참고 템플릿

@templates/plugin-template.md — Plugin 디렉토리 구조 템플릿. 실습 시 참고용으로 안내할 수 있다.
