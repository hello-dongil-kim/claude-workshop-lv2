# Claude Workshop Lv.2 — 비개발자를 위한 Claude Code 확장

> **대상:** Claude Code를 처음 확장하는 비개발자 (기획자, UX 리서처, PM 등)
> **전제:** Claude Code 설치 완료 + 기본 대화 경험 (프롬프트 입력 → 결과 확인 수준)
> **총 소요:** 약 2시간 51분 (세션 4개 + 워크숍 1개)
> **핵심 메타포:** Claude Code = "나만의 팀을 조직하는 것"

---

## 핵심 요약 — 꼭 해야 할 것 vs 하지 말아야 할 것

| 구분 | 항목 | 이유 |
| ---- | ---- | ---- |
| ✅ DO | **폴더 단위로 작업 시작** | Claude Code는 폴더 전체를 보고 작업. 파일 하나만 올리면 맥락을 놓침 |
| ✅ DO | **`/init`으로 CLAUDE.md 생성 후 직접 다듬기** | 매 세션 자동 로드되는 '작업 매뉴얼'. 한 번 써두면 반복 설명 불필요 |
| ✅ DO | **CLAUDE.md는 200줄 이내로 유지** | 길면 Claude가 지침을 놓치는 비율이 급격히 증가 |
| ✅ DO | **작업이 바뀔 때마다 `/clear`** | 이전 작업 내용이 쌓이면 성능이 떨어짐 |
| ✅ DO | **복잡한 작업은 Plan Mode로 먼저 탐색** | 읽기 전용이라 안전. 잘못된 방향 실행 예방 |
| ✅ DO | **프롬프트에 형식·분량·저장 위치를 구체적으로 지정** | "잘 정리해줘"는 결과가 매번 다름 |
| ✅ DO | **탐색·조사는 서브에이전트에 위임** | 탐색 과정이 메인 대화를 오염시키지 않음 |
| ✅ DO | **반복 작업은 Skills로 자동화** | 한 번 만들어두면 이후 한 줄로 실행 |
| ✅ DO | **결과물은 기대치와 비교 검증** | AI는 그럴듯한 환각을 만들 수 있음 |
| ❌ DON'T | **한 세션에 관련 없는 여러 작업 섞기** | 이전 작업 잔여물이 현재 작업에 영향 |
| ❌ DON'T | **같은 문제를 2회 이상 같은 대화에서 고치기** | `/clear` 후 재시작이 빠름 |
| ❌ DON'T | **CLAUDE.md를 한 번 쓰고 방치** | 현재 상황과 어긋나면 잘못된 방향으로 유도 |
| ❌ DON'T | **범위 없이 "다 찾아봐" 식 요청** | 무한 탐색으로 컨텍스트·비용 낭비 |
| ❌ DON'T | **Plan Mode 건너뛰고 바로 실행** | 복잡한 작업일수록 잘못된 수정 위험 |
| ❌ DON'T | **결과물을 검증 없이 수락** | 환각·오탈자·잘못된 수치가 그대로 최종본에 남음 |
| ❌ DON'T | **Bypass permissions를 기본 모드로 사용** | 모든 작업 자동 승인 → 되돌리기 어려운 변경 발생 |

---

## 이 과정을 마치면

- CLAUDE.md로 프로젝트 맥락을 설계할 수 있다
- Skills로 전문 지식을 자동 로딩할 수 있다
- MCP로 외부 도구(Notion, Slack, Gmail 등)를 연결할 수 있다
- Subagent로 보조 작업을 위임할 수 있다
- 이 모든 것을 Plugin으로 팀에 배포할 수 있다

> **사내 도구 연동:** 회사에서 Confluence·Jira 같은 사내 도구를 쓴다면, Lv.2 완료 후 회사 내부의 사내 연동 가이드를 따라 Claude Code에 연결할 수 있습니다. Session 3(MCP)에서 배우는 개념이 그대로 적용됩니다.

## 기대 효과

### 세션별 역량 변화

| 세션 | Before | After |
| ---- | ------ | ----- |
| **S1** | 매 세션마다 같은 설명 반복, 작업 방식 비효율 | 프로젝트 규칙 자동 적용 + 4단계 워크플로우로 체계적 작업 |
| **S2** | 도메인 전문 지식을 매번 프롬프트에 입력 | 대화 키워드에 따라 전문 지식이 자동 로딩 |
| **S3** | Notion/Slack 내용을 수동 복붙 | Claude가 외부 도구에 직접 접근 + 품질 체크 자동화 |
| **S4** | 리서치·분석을 혼자 순차적으로 처리 | 전문 에이전트에게 위임하여 병렬 처리 |
| **WS** | 워크플로우를 팀원마다 개별 세팅 | 한 번 패키징하면 팀 전원 일괄 설치 |

### 핵심 산출물

이 과정을 마치면 아래 산출물을 직접 만들어 보유하게 됩니다:

1. **나만의 CLAUDE.md** — 프로젝트 규칙서 (언어, 포맷, 톤, 산출물 구조)
2. **Skill 파일 1~2개** — 자주 하는 업무의 전문 지식 자동 로딩
3. **MCP 서버 1개 연결** — Notion/Slack/Gmail 등 실제 도구 연동
4. **Hook 설정 1개** — 산출물 자동 백업, 포맷 검증 등
5. **Subagent 설계 1개** — 리서치/분석 등 보조 작업 위임 구조

### 비개발자에게 특히 유용한 이유

이 과정은 코딩 부트캠프가 아닙니다. **여러분이 이미 잘 하는 "문서로 설계하기"가 그대로 Claude Code 확장 역량이 되는 과정**입니다.

| 여러분의 기존 역량 | Claude Code에서의 활용 |
| ----------------- | --------------------- |
| 프로세스 문서 작성 | CLAUDE.md — 한 번 쓰면 항상 적용 |
| 템플릿 설계 | SKILL.md — 맥락에 맞게 자동 로딩 |
| 체크리스트 만들기 | Hooks — 자동 실행 품질 체크 |
| 팀원에게 업무 위임 | Subagents — 구조적 작업 위임 |
| 팀 표준 배포 | Plugins — 원클릭 설치 패키지 |

모든 확장 기능은 **마크다운 문서와 JSON 설정 파일**로 구성됩니다. 코딩 경험이 없어도 즉시 시작할 수 있습니다.

---

## 환경 전환 안내

> **Lv.1에서 오셨나요?** Lv.1은 Claude 앱(웹/데스크톱)에 파일을 첨부하여 진행했습니다. **Lv.2부터는 Claude Code 안에서 진행합니다.** 환경이 완전히 바뀌므로 아래 사항을 확인하세요:
>
> | 항목 | Lv.1 | Lv.2 |
> | ---- | ---- | ---- |
> | 실행 환경 | Claude 앱 (웹/데스크톱) | Claude Code (IDE / 터미널 / 데스크톱 앱 Code 탭 / 웹 앱) |
> | 튜터 구동 | 파일 첨부 → "실행해줘" | 폴더 열기 → Claude Code 패널/터미널에서 `/session1-claude-md` 입력 |
> | 파일 생성 | 대화창에 텍스트 출력 | 내 폴더에 실제 파일 생성 |
> | 진행 방식 | 동일 (2Phase: 설명→퀴즈) | 동일 |

## 사전 준비

| 항목 | 요구사항 |
| ---- | -------- |
| Claude Code | 설치 완료 (IDE 확장, 데스크톱 앱, 웹 앱, CLI 중 하나) |
| 계정 | Claude Pro, Max, Teams, Enterprise 중 하나 |
| OS | macOS 13.0+ / Windows 10 (1809)+ |
| IDE | VS Code (권장), Cursor, Google Antigravity 등 VS Code 기반 IDE. 또는 데스크톱 앱/웹 앱(claude.ai/code) |
| 인터넷 | 필요 |

---

## 사용 환경

IDE, 터미널, 또는 데스크톱 앱 중 편한 환경에서 진행합니다. **`/` 명령어와 대화 방식은 모든 환경에서 동일**합니다.

### A. IDE (VS Code 권장)

| 단계 | 방법 |
| ---- | ---- |
| **시작** | IDE에서 claude-workshop-lv2 폴더 열기 (File → Open Folder) → Claude Code 패널 자동 활성화 |
| **대화** | Claude Code 패널의 입력창에 메시지 또는 `/` 명령어 입력 |
| **새 세션** | 패널 상단 `+` 버튼 또는 `New Chat` |
| **파일 확인** | 에디터에서 바로 열림 — 변경사항을 실시간으로 볼 수 있어 편리 |
| **터미널 명령** | IDE 내장 터미널 사용 (예: `claude mcp add ...`) |

### B. 터미널 (CLI)

| 단계 | 방법 |
| ---- | ---- |
| **시작** | `cd [claude-workshop-lv2 경로]` → `claude` |
| **대화** | 터미널에서 직접 메시지 또는 `/` 명령어 입력 |
| **새 세션** | `exit`으로 종료 → `claude`로 재시작, 또는 새 터미널 탭 |
| **파일 확인** | `cat`, `open` 명령어 또는 별도 에디터에서 확인 |
| **터미널 명령** | 현재 터미널에서 바로 실행 |

### C. 데스크톱 앱 (3탭 구조)

데스크톱 앱은 Chat / Code / Cowork 3탭으로 구성됩니다. 이 워크숍은 **Code 탭**에서 진행합니다.

| 탭 | 용도 | 워크숍 진행 |
| --- | --- | --- |
| **Chat** | 파일 없이 일반 대화 | — |
| **Code** | 폴더를 열고 파일 직접 읽기/수정 | **이 탭에서 진행** |
| **Cowork** | 클라우드 VM에서 백그라운드 독립 작업 | Session 4에서 다룸 |

---

## 시작하기

환경을 열고, Claude Code에서 아래를 입력합니다:

```text
/session1-claude-md
```

또는 자연어로:

```text
세션 1 시작해줘
```

---

## 커리큘럼

```text
Session 1  →  Session 2  →  Session 3  →  Session 4  →  Workshop
 CLAUDE.md      Skills      MCP & Hooks     Agents       Plugins
  ★☆☆☆☆       ★★★☆☆       ★★★★☆        ★★★★★        실습
  ~46분         ~35분         ~30분          ~35분         ~25분
```

| 세션 | 주제 | 블록 | 산출물 | 시작 명령 |
| ---- | ---- | ---- | ------ | --------- |
| **S1** | CLAUDE.md — 프로젝트 브리핑 + 핵심 워크플로우 | 4 | 나만의 CLAUDE.md | `/session1-claude-md` |
| **S2** | Skills — 자동 로딩 전문 지식 | 3 | Skill 파일 1개 | `/session2-skills` |
| **S3** | MCP & Hooks — 도구·자동화 | 3 | MCP 연결 + Hook 설정 | `/session3-mcp-hooks` |
| **S4** | Agents — 작업 위임 | 3 | Subagent 설계 | `/session4-agents` |
| **WS** | Plugins — 팀에 배포하기 | 2 | 나만의 Skill 완성 | `/workshop-plugins` |

---

## 진행 방법

### 1. 블록 선택

세션을 시작하면 블록 목록이 표시됩니다. 처음이면 Block 0부터 순서대로 진행하세요.

### 2. 2-Phase 진행

각 블록은 **2턴**으로 진행됩니다:

| Phase | 내용 | 사용자 액션 |
| ----- | ---- | ---------- |
| **A** | 개념 설명 + 실습 안내 | 직접 실행해보기 |
| **B** | 퀴즈 | 정답 선택 → 피드백 → 다음 블록 |

실행이 끝나면 "완료" 또는 "다음"이라고 입력하세요.

### 3. 세션 간 이동

순서대로 진행을 추천합니다. 이미 아는 내용이면 건너뛰어도 됩니다.

---

## 전체 확장 기능 계층 구조

```text
Plugins (배포·패키징)
  └ Agent Teams (병렬 협업)
    └ Subagents (독립 위임)
      └ Hooks (자동화) + MCP (도구 연결)
        └ Skills (자동 로딩 지식)
          └ CLAUDE.md (기본)
```

---

## 파일 구조

```text
claude-workshop-lv2/
├── README.md
└── .claude/skills/
    ├── session1-claude-md/        ★☆☆☆☆  ~46분
    │   ├── SKILL.md
    │   ├── references/ (4)
    │   └── templates/ (1)
    ├── session2-skills/           ★★★☆☆  ~35분
    │   ├── SKILL.md
    │   ├── references/ (3)
    │   └── templates/ (1)
    ├── session3-mcp-hooks/        ★★★★☆  ~30분
    │   ├── SKILL.md
    │   ├── references/ (3)
    │   └── templates/ (1)
    ├── session4-agents/           ★★★★★  ~35분
    │   ├── SKILL.md
    │   ├── references/ (3)
    │   └── templates/ (1)
    └── workshop-plugins/          실습    ~25분
        ├── SKILL.md
        ├── references/ (2)
        └── templates/ (1)
```

---

## 학습 진도 추적

각 세션을 시작하면 블록 목록이 표시됩니다. 완료한 블록을 기억하기 어렵다면, 아래 체크리스트를 활용하세요:

```text
[ ] S1 Block 0: CLAUDE.md 개념 + 권한 모드 + 컨텍스트 관리
[ ] S1 Block 1: CLAUDE.md 실습 + 4단계 워크플로우
[ ] S1 Block 2: 프롬프트 패턴 + 메모리 + 비용 관리 + 팀 공유
[ ] S1 Block 3: 프로젝트 구조 전체 맵
[ ] S2 Block 0: Skills 개념 (vs Commands)
[ ] S2 Block 1: SKILL.md 구조 (description 설계)
[ ] S2 Block 2: 나만의 첫 Skill 만들기
[ ] S3 Block 0: MCP 개념 + 연결
[ ] S3 Block 1: Hooks 개념 + 4가지 시점
[ ] S3 Block 2: MCP + Hook 실습
[ ] S4 Block 0: Subagent 개념 + Cowork 탭 백그라운드 실행
[ ] S4 Block 1: Subagent 설계
[ ] S4 Block 2: Agent Teams + /batch 병렬 실행
[ ] WS Block 0: Plugin 개념 + 탐색
[ ] WS Block 1: 플러그인 체험 + 나만의 Skill
```

> **팁:** 이 체크리스트를 복사해서 프로젝트 폴더에 `progress.md`로 저장하면, 다음에 이어서 진행할 때 편합니다.

---

## 빠른 시작 체크리스트

Claude Code를 처음 시작하는 분을 위한 순서:

- [ ] **1단계**: Claude Code 환경 준비 (IDE 확장, 데스크톱 앱, 웹 앱, CLI 중 하나)
- [ ] **2단계**: claude-workshop-lv2 폴더 열기 (IDE: File → Open Folder / 터미널: `cd` → `claude`)
- [ ] **3단계**: `/init` 입력하여 CLAUDE.md 자동 생성
- [ ] **4단계**: CLAUDE.md에 본인의 역할, 선호 형식, 작업 맥락 추가
- [ ] **5단계**: Plan mode로 전환 후 첫 작업 탐색
- [ ] **6단계**: Ask permissions 모드로 전환 후 간단한 작업 실행
- [ ] **7단계**: 사내 도구(위키·이슈 트래커 등) 연동 (Session 3에서 상세히 다룸)
- [ ] **8단계**: 반복 작업이 생기면 Skills로 자동화 (Session 2에서 상세히 다룸)
- [ ] **9단계**: 작업 위임이 필요하면 Subagent / `/batch` / Cowork 탭 활용 (Session 4에서 상세히 다룸)

---

## 문제 해결

| 증상 | 해결 |
| ---- | ---- |
| 스킬이 인식되지 않음 | IDE에서 claude-workshop-lv2 폴더를 열었는지 확인 (File → Open Folder) |
| `/session1-claude-md`가 안 됨 | Claude Code 패널에서 `/` 입력 후 자동완성 목록 확인 |
| 퀴즈가 Phase A에서 나옴 | "STOP PROTOCOL을 따라줘"라고 리마인드 |
| 블록을 건너뛰고 싶음 | 시작 시 원하는 블록 번호를 선택하면 됨 |

---

## 만든 사람

**김동일 (Dongil Kim)**

- Email: <hello@dongil.kim>
- LinkedIn: <https://www.linkedin.com/in/hellodongilkim/>
- GitHub: <https://github.com/hello-dongil-kim/>
