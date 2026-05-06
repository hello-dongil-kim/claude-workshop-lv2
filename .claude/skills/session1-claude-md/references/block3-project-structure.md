# Block 3: 프로젝트 구조 전체 맵

## EXPLAIN

### Claude Code 프로젝트의 전체 구조

CLAUDE.md는 시작일 뿐이다. Claude Code 프로젝트에는 더 많은 설정 파일과 확장 폴더가 있다. 전체 그림을 먼저 보고, 이후 세션에서 하나씩 파고들자.

```text
your-project/
├── CLAUDE.md              ← 팀 공통 규칙 (Git 커밋)
├── CLAUDE.local.md        ← 개인 규칙 (Git 무시)
└── .claude/
    ├── settings.json      ← 권한 + MCP + Hook 설정 (Git 커밋)
    ├── settings.local.json ← 개인 권한 설정 (Git 무시)
    ├── commands/          ← 수동 호출 슬래시 명령어
    ├── rules/             ← 자동 로딩 규칙 파일
    ├── skills/            ← 자동 트리거 워크플로우
    └── agents/            ← 독립 컨텍스트 서브에이전트
```

### CLAUDE.md 4단계 우선순위 — 어디에 둘 수 있나

CLAUDE.md는 위치에 따라 적용 범위와 강제력이 다르다. 우선순위가 높은 순서로:

| 순위 | 위치 | Git | 강제력 | 용도 |
| ---- | ---- | --- | ---- | ---- |
| **1** | 관리 정책 CLAUDE.md | — | 개인 해제 불가 | 조직 전체 보안·컴플라이언스 |
| **2** | `./CLAUDE.local.md` | 무시 | 개인만 적용 | 나만의 스타일·환경 — "내 Jira 계정 XXX, 마케팅팀 소속" |
| **3** | `./CLAUDE.md` | 커밋 | 팀 전원 적용 | 팀 공유 — "이 프로젝트는 SaaS 경쟁사 분석용. output/ 폴더에 저장" |
| **4** | `~/.claude/CLAUDE.md` | — | 내 모든 프로젝트 | 글로벌 — "항상 한국어 답변. 보고서는 마크다운 표 활용" |

> **충돌 시 동작:** 위 순위대로 합쳐지며, 같은 항목이 충돌하면 **상위 순위가 우선**한다. 즉 관리 정책 → 개인 local → 프로젝트 → 글로벌 순으로 강제력이 약해진다.

**활용 예시:**

- `~/.claude/CLAUDE.md` — 모든 프로젝트 공통: "한국어, 마크다운, 선택지+추천안 형식"
- `./CLAUDE.md` — 이 프로젝트 한정: "경쟁사 분석 프레임워크는 5 Forces 사용"
- `./CLAUDE.local.md` — 나만의 환경: "내 Jira 계정 ID, 즐겨쓰는 출처 URL"

> **settings.json도 같은 원리:** 권한·MCP·Hook 설정도 `settings.json`(Git 커밋, 팀 공유)과 `settings.local.json`(Git 무시, 개인 전용)으로 나뉜다. 즉 **규칙 문서(CLAUDE.md)와 설정 파일(settings.json) 모두 "팀 공유 + 개인 전용" 2개 짝 구조**다.

### .claude/ 폴더의 4가지 확장 폴더

| 폴더 | 역할 | 호출 방식 | 예시 (기획자용) |
| ---- | ---- | --------- | -------------- |
| **commands/** | 슬래시 명령어 | `/명령어`로 수동 호출 | `/review-prd`, `/weekly-report` |
| **rules/** | 모듈화된 규칙 | 매 세션 자동 로딩 | output-format.md, research-standards.md |
| **skills/** | 전문 워크플로우 | 대화 맥락에 따라 자동 트리거 | ux-research/, service-planning/ |
| **agents/** | 서브에이전트 | `@에이전트명`으로 호출 (독립 컨텍스트) | desk-researcher, meeting-scribe |

### commands/ vs rules/ — 헷갈리는 두 폴더

둘 다 `.md` 파일이지만 동작이 완전히 다르다:

| 구분 | commands/ | rules/ |
| ---- | --------- | ------ |
| 로딩 시점 | `/명령어` 입력 시에만 | 매 세션 시작 시 항상 |
| 비유 | "이거 해줘" 버튼 | CLAUDE.md의 분리된 페이지 |
| 예시 | `/review-prd` → PRD 검토 프롬프트 실행 | research-standards.md → 리서치 품질 기준 항상 적용 |
| 특징 | 인자 전달 가능 (`/명령어 인자`) | CLAUDE.md가 길어질 때 주제별로 분리 |

**rules/는 CLAUDE.md의 확장**이다. CLAUDE.md가 200줄에 가까워지면, 주제별로 rules/ 파일로 분리하여 관리할 수 있다.

### 이후 세션과의 연결

| 폴더 | 다루는 세션 |
| ---- | ---------- |
| commands/ | 이번 세션에서 개념만 소개. Skill이 상위 호환이므로 Session 2에서 비교 |
| rules/ | CLAUDE.md의 확장 — 이번 세션에서 개념 소개 |
| skills/ | **Session 2**에서 깊이 다룸 |
| agents/ | **Session 4**에서 깊이 다룸 |
| settings.json | **Session 3**에서 MCP/Hook 맥락으로 다룸 |

---

## EXECUTE

다음을 직접 실행해보세요:

**Step 1: 현재 프로젝트 구조 확인**

```text
.claude/ 폴더 안에 어떤 파일과 폴더가 있는지 보여줘
```

**Step 2: Commands 체험**

```text
.claude/commands/ 폴더에 어떤 명령어가 있는지 확인하고,
하나를 실행해봐
```

- `/` 입력 후 자동완성 목록에서 사용 가능한 명령어를 확인

**Step 3: Rules 개념 확인**

```text
.claude/rules/ 폴더가 있는지 확인해줘.
있으면 어떤 규칙 파일이 있는지 보여줘.
```

- 없으면 정상 — 필요할 때 만들면 된다

---

## QUIZ

**문제:** .claude/ 폴더 안의 commands/와 rules/의 차이는?

| 선택지 | 내용 |
|--------|------|
| A | commands/는 Git에 커밋하고, rules/는 .gitignore에 넣는다 |
| B | commands/는 `/명령어`로 수동 호출하고, rules/는 매 세션 자동으로 읽힌다 |
| C | commands/는 팀 공용이고, rules/는 개인 전용이다 |

**정답:** B — commands/의 파일은 `/파일명`으로 직접 호출할 때만 실행된다. rules/의 파일은 CLAUDE.md처럼 매 세션 자동 로딩되되, 주제별로 파일을 분리할 수 있다. 둘 다 Git 커밋 대상이고 팀 공용이다.
