# Block 0: Plugin 개념 + 탐색

## EXPLAIN

### Plugin이란?

지금까지 배운 확장 기능들을 떠올려 보자:

| Session | 배운 것 | 역할 |
|---------|---------|------|
| 1 | CLAUDE.md | 프로젝트 규칙서 |
| 2 | Skills | 자동 로딩 지식 |
| 3 | MCP / Hooks | 외부 도구 연결 / 자동화 |
| 4 | Subagents / Agent Teams | 독립 위임 / 병렬 협업 |

이것들을 **하나의 패키지**로 묶어서 설치/공유할 수 있다면? 그것이 바로 **Plugin**이다.

**Plugin = Skills + Commands + Subagents를 하나의 패키지로 묶어 설치/공유하는 단위**

### 비유: 앱스토어

| 비유 | 실제 |
|------|------|
| 앱스토어에서 앱 검색 | Marketplace에서 플러그인 검색 |
| 앱 설치 (한 번 탭) | `/plugin install` (한 번 실행) |
| 앱 안에 여러 기능이 묶여 있음 | 플러그인 안에 Skills + Commands + Subagents가 묶여 있음 |
| 앱 업데이트 | 플러그인 버전 업데이트 |
| 앱 삭제 | 플러그인 제거 |

누군가가 만든 워크플로우를 **한 번에 설치**해서 바로 사용할 수 있다. 하나하나 파일을 복사하고 설정할 필요가 없다.

### 왜 Plugin이 필요한가?

**문제 1: 수동 세팅의 고통**
- 팀원 5명이 같은 Skill을 쓰려면, 5명 모두 SKILL.md를 복사하고 폴더를 만들어야 한다
- 누군가 빠뜨리면 작동이 안 되고, 버전이 달라지면 결과가 다르다

**문제 2: 네임스페이스 충돌**
- 두 사람이 각각 `write-prd`라는 Skill을 만들면 이름이 겹친다
- Plugin은 `pm-skills:write-prd`, `my-team:write-prd`처럼 **네임스페이스**로 구분한다

**문제 3: 버전 관리**
- Skill을 개선했는데, 팀원 중 절반은 구버전을 쓰고 있다
- Plugin은 Git 저장소 기반이라 `git pull` 한 번이면 전원 최신 버전으로 동기화

### Plugin의 구조

Plugin은 Marketplace(GitHub 저장소)에 등록된다:

```
marketplace-repo/                # GitHub 저장소 (마켓플레이스)
├── .claude-plugin/
│   └── marketplace.json        # 마켓플레이스 카탈로그 (어떤 플러그인이 있는지)
└── my-plugin/                   # 플러그인 1개
    ├── .claude-plugin/
    │   └── plugin.json         # 플러그인 매니페스트 (이 폴더 안에만)
    ├── skills/                 # Skills 모음
    │   ├── skill-a/
    │   │   └── SKILL.md
    │   └── skill-b/
    │       ├── SKILL.md
    │       └── references/
    ├── commands/               # Commands 모음
    │   └── my-command.md
    └── agents/                 # Subagents 모음
        └── my-agent.md
```

> **핵심:** 매니페스트(`plugin.json`)와 마켓플레이스 카탈로그(`marketplace.json`)만 `.claude-plugin/` 폴더 안에 두고, `skills/`·`commands/`·`agents/`는 플러그인 루트에 둔다.

### 설치/탐색 핵심 명령어

> 📌 **변동 정보 (최종 확인: 2026-06-14)** — 아래 플러그인 명령어 형식(`/plugin install` 등)과 매니페스트 위치(`plugin.json`은 `.claude-plugin/` 안)는 바뀔 수 있습니다. 최신값은 공식 문서(https://docs.claude.com)를 확인하세요.

| 명령어 | 설명 |
|--------|------|
| `/plugins` | 현재 설치된 플러그인 목록 확인 |
| `/plugin marketplace add {URL}` | 마켓플레이스 저장소 추가 |
| `/plugin install {이름}` | 플러그인 설치 |
| `/plugin uninstall {이름}` | 플러그인 제거 |

설치하면 해당 Plugin 안의 모든 Skills, Commands, Subagents가 한 번에 사용 가능해진다.

> **⚠️ 안전 베이스라인:** 플러그인은 다른 사람의 Skills·Commands·Subagent를 한꺼번에 들여오는 것이다. **신뢰할 수 있는 마켓플레이스(출처가 분명한 GitHub 저장소)만 추가·설치**하고, 설치 후 어떤 스킬·명령이 들어왔는지 `/plugins`로 한 번 확인하는 습관을 들이자.

### 네임스페이스 규칙

Plugin을 설치하면 스킬명 앞에 **플러그인 이름이 네임스페이스로 붙는다**:

```
플러그인명:스킬명
```

예시:

- `pm-skills:write-prd` — pm-skills 플러그인의 PRD 작성 스킬
- `pm-skills:sprint-plan` — pm-skills 플러그인의 스프린트 계획 스킬
- `superpowers:brainstorming` — superpowers 플러그인의 브레인스토밍 스킬

이 규칙 덕분에 서로 다른 플러그인에 같은 이름의 스킬이 있어도 충돌하지 않는다.

---

## EXECUTE

다음을 직접 실행해보세요:

**Step 1: 설치된 플러그인 확인**
```
/plugins
```
- 현재 어떤 플러그인이 설치되어 있는지 확인
- 각 플러그인 안에 어떤 Skills/Commands가 포함되어 있는지 살펴보기

**Step 2: 네임스페이스 확인**
- 설치된 스킬 목록을 보면서 `플러그인명:스킬명` 형식을 확인
- 예: `pm-skills:write-prd`, `superpowers:brainstorming` 등

**Step 3: (선택) 마켓플레이스 둘러보기**
- 사용 가능한 마켓플레이스가 있다면 어떤 플러그인들이 있는지 탐색

> ✅ **이렇게 되면 성공:** `/plugins`로 설치된 플러그인 목록을 보고, 스킬 이름이 `플러그인명:스킬명` 형식(네임스페이스)으로 표시되는 것을 한 개 이상 찾아내면 성공.

---

## QUIZ

**문제 1 (회상형):** Plugin이 해결하는 핵심 문제는?

| 선택지 | 내용 |
|--------|------|
| A | 여러 프로젝트에서 같은 CLAUDE.md를 공유할 수 있게 한다 |
| B | 외부 API를 연결해준다 |
| C | Skills/Commands/Subagents를 패키지로 묶어 설치/공유/버전 관리를 통합한다 |

**정답:** C — Plugin은 여러 확장 기능(Skills, Commands, Subagents)을 하나의 패키지로 묶어서, 한 번의 설치로 전체 워크플로우를 배포하고, 네임스페이스로 충돌을 방지하며, Git 기반 버전 관리를 가능하게 한다. CLAUDE.md 공유는 Git 커밋으로, 외부 API 연결은 MCP의 역할이다.
- A 오답: CLAUDE.md 공유는 Git 커밋으로 해결한다 — Plugin의 핵심 목적이 아니다.
- B 오답: 외부 API 연결은 MCP의 역할이다 — Plugin은 확장 기능 패키징·배포 도구다.

**문제 2 (적용형):** 다음 상황에서 가장 적절한 것은? — 팀원 두 명이 각각 `write-prd` Skill을 만들었는데 이름이 똑같아 충돌한다. 둘 다 살리고 싶다.

| 선택지 | 내용 |
|--------|------|
| A | 한 명이 스킬 이름을 `write-prd2`로 바꾼다 |
| B | 각자 자기 Plugin으로 묶으면 `팀A:write-prd`, `팀B:write-prd`처럼 네임스페이스로 구분된다 |
| C | 둘 중 하나를 삭제한다 |

**정답:** B — Plugin으로 묶으면 스킬 앞에 `플러그인명:`이 붙어, 같은 이름이라도 충돌하지 않고 둘 다 쓸 수 있다.
- A 오답: 이름을 억지로 바꾸면 임시방편일 뿐, 근본적인 충돌 방지 메커니즘이 아니다.
- C 오답: 하나를 버리면 둘 다 살리려던 목적에 어긋난다.
