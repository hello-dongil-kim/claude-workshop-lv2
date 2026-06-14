---
name: session4-agents
description: |
  Subagents & Agent Teams 실습. "Subagent", "에이전트 팀", "위임", "Agent Teams", "세션 4", "Session 4" 키워드에 트리거.
  비개발자를 위한 작업 위임 구조를 배우고 직접 설계한다.
---

# Session 4. Subagents & Agent Teams — "일을 구조적으로 위임하기"

> **난이도:** ★★★★★ | **소요:** ~35분 | **블록:** 3개
> **대상:** Claude Code를 확장하려는 기획자, UX 리서처, PM
> **전제:** Claude Code 기본 사용 경험, CLAUDE.md 및 Skill 개념 이해

## 용어 정리

| 용어 | 설명 |
|------|------|
| **Subagent** | 별도 컨텍스트 윈도우에서 독립 작업 후 결과만 돌려주는 Claude 인스턴스 |
| **Agent Teams** | 여러 전문 에이전트가 수평적으로 병렬 협업하는 구조 (실험적 기능) |
| **컨텍스트 오염** | 메인 대화에 불필요한 중간 과정이 쌓여 품질이 떨어지는 현상 |
| **Task tool** | Plan mode에서 Subagent를 호출하는 내부 도구 |

---

## 진도 관리 — 시작 시 먼저 확인

세션을 시작하면 **블록 선택 전에** 아래를 처리한다:

1. **이어하기 확인** — 프로젝트 루트에 `progress.md`가 있으면 읽고, 완료된 S4 블록을 보여준 뒤 "이어서 다음 블록부터 진행할까요?"라고 제안한다. 없으면 그냥 Block 0부터 안내한다.
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
| 0 | Subagent 개념 | Subagent란? + 비유 + 호출 방식 + 내장 에이전트 | ~12분 |
| 1 | Subagent 설계 | 기획자용 에이전트 설계 + 직접 체험 | ~13분 |
| 2 | Agent Teams | 개념 + 기획 시나리오 + Subagent vs Teams 비교 | ~10분 |

처음이면 Block 0부터 순서대로 진행을 추천한다.

---

## Block 0: Subagent 개념

@references/block0-subagent-concept.md 파일의 EXPLAIN → EXECUTE → QUIZ 순서로 진행.

## Block 1: Subagent 설계

@references/block1-subagent-design.md 파일의 EXPLAIN → EXECUTE → QUIZ 순서로 진행.

## Block 2: Agent Teams

@references/block2-agent-teams.md 파일의 EXPLAIN → EXECUTE → QUIZ 순서로 진행.
