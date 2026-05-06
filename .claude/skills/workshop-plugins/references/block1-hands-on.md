# Block 1: 실습 — 플러그인 체험 + 나만의 Skill 만들기

## EXPLAIN

### 기획 조직에서의 Plugin 활용 시나리오

Plugin은 팀 단위로 워크플로우를 표준화할 때 진가를 발휘한다. 기획 조직에서 활용할 수 있는 3가지 시나리오를 살펴보자.

#### 시나리오 1: UX 리서치 팀 표준

```
ux-research-plugin/
├── skills/
│   └── research-brief/          # 리서치 브리프 작성 Skill
│       └── SKILL.md             # 리서치 목적, 대상, 방법론 구조화
├── commands/
│   └── interview-guide.md       # /interview-guide — 인터뷰 가이드 생성
└── agents/
    └── insight-analyzer/        # 인터뷰 데이터 → 인사이트 추출 Subagent
        └── SKILL.md
```

**효과:** 팀원 누구나 같은 형식의 리서치 브리프를 작성하고, 인터뷰 가이드를 생성하고, 분석 결과를 일관된 포맷으로 받을 수 있다.

#### 시나리오 2: 서비스 기획 팀 표준

```
service-planning-plugin/
├── skills/
│   └── prd-template/            # PRD 작성 Skill
│       ├── SKILL.md             # 팀 PRD 구조에 맞춘 자동 생성
│       └── references/
│           └── prd-format.md    # 팀 PRD 표준 포맷
├── commands/
│   └── competitor-scan.md       # /competitor-scan — 경쟁사 빠른 분석
└── agents/
    └── spec-reviewer/           # 스펙 문서 품질 리뷰 Subagent
        └── SKILL.md
```

**효과:** PRD의 구조가 팀 전체에서 통일되고, 경쟁사 분석 프로세스가 표준화되며, 스펙 리뷰를 자동으로 받을 수 있다.

#### 시나리오 3: PMO 거버넌스

```
pmo-governance-plugin/
├── skills/
│   └── launch-checklist/        # 출시 체크리스트 Skill
│       └── SKILL.md             # 출시 전 필수 확인 항목 자동 점검
├── commands/
│   └── kpi-dashboard.md         # /kpi-dashboard — KPI 현황 요약
└── agents/
    └── quality-auditor/         # 산출물 품질 감사 Subagent
        └── SKILL.md
```

**효과:** 출시 전 체크리스트 누락이 사라지고, KPI 현황을 빠르게 파악하며, 산출물 품질을 자동으로 감사받을 수 있다.

### 전체 확장 기능 계층 구조

Session 1부터 Workshop까지 배운 모든 것의 계층 관계:

```text
Plugins (배포/패키징)
  └ Agent Teams (병렬 협업)
    └ Subagents (독립 위임)
      └ Hooks (자동화) + MCP (도구 연결)
        └ Skills (자동 로딩 지식)
          └ CLAUDE.md (기본)
```

아래에서 위로 쌓아 올린 것이다:

1. **CLAUDE.md** — 프로젝트 규칙을 정의하고
2. **Skills** — 전문 지식을 자동 로딩하고
3. **Hooks + MCP** — 외부 도구를 연결하고 자동화하고
4. **Subagents** — 독립된 작업을 위임하고
5. **Agent Teams** — 여러 에이전트가 협업하고
6. **Plugins** — 이 모든 것을 패키지로 묶어 배포한다

### 실전 사례 참고: 다른 사람들은 이런 Skill을 만들었다

Session 1~4를 마쳤으니, 실전에서 쓰이는 Skill 사례를 먼저 보자:

**사례 1: 미팅 정리 Skill** — 녹취록을 붙여넣으면 30초 만에 회의록 완성
- 요청: "녹취록을 주면 참석자, 핵심 안건 3~5개, 결정사항, 액션아이템(담당자+기한 테이블), 미결 사항으로 정리해줘"
- 효과: 팀원 전원이 같은 포맷의 회의록 사용. 지난 회의 결정사항 검색 용이

**사례 2: 블로그 아티클 Skill** — 데이터만 넣으면 발행 가능한 글이 나온다
- 요청: "사례 데이터(계정명, 조회수, 콘텐츠 링크)를 주면 인사이트 아티클을 작성해줘. 사례는 절대 지어내지 말 것. 톤앤매너 가이드는 references/에 별도 저장"
- 효과: 반나절 → 30분. references/에 톤앤매너 가이드를 넣어서 다른 팀원이 써도 같은 퀄리티

> **공통점:** 반복 작업 + 우리만의 규칙 + 일관성 필요. Session 2에서 배운 "판단 체크리스트 4가지" 중 3개 이상 해당하는 작업들이다.

### 실습 과제: 나만의 첫 번째 Skill 만들기

Session 1~4에서 배운 것을 종합하여, **자신의 업무에 적용할 Skill 1개**를 직접 만들어 본다.

**Skill 설계 3단계:**

**1단계: 반복 프롬프트 선정**
- 자신이 Claude에게 자주 요청하는 것 중 가장 반복적인 프롬프트 1개를 고른다
- 예: "회의록 정리해줘", "PRD 초안 써줘", "경쟁사 비교해줘", "사용자 인터뷰 정리해줘"

**2단계: Claude에게 5요소로 요청**
```text
{작업명} Skill을 만들어줘.
@templates/skill-template.md 를 참고해서 .claude/skills/ 에 생성해줘.

작업 정의: {이 Skill이 할 일}
트리거 상황: {키워드 3~5개}
규칙: {핵심 규칙}
톤: {결과물 말투}
결과물 형태: {산출물 구조}
```

**3단계: 품질 체크 + 테스트**
- description에 트리거 키워드가 있는지 확인
- 1 Skill = 1 역할인지 확인
- 자동 호출 + `/스킬명` 수동 호출 테스트

---

## EXECUTE

다음을 직접 실행해보세요:

**Step 1: 플러그인 설치 체험**
- `/plugins`로 현재 상태 확인
- 사용 가능한 플러그인 중 하나를 설치해 보기 (설치 후 스킬 목록 변화 확인)

**Step 2: 나만의 Skill 만들기 (최종 실습)**
1. 가장 자주 반복하는 프롬프트 1개를 선정
2. `.claude/skills/{스킬명}/SKILL.md` 파일 작성
   - description에 트리거 키워드를 포함시킬 것
   - 역할, 작업 규칙, 산출물 형식을 구체적으로 정의할 것
3. 파일 저장

**Step 3: 테스트**
- 트리거 키워드로 대화를 시작하여 스킬이 자동 로딩되는지 확인
- 산출물이 의도한 형식대로 나오는지 확인

**Step 4: 캡스톤 과제 — 나의 3-Skill 워크플로우 설계**

Session 1~4에서 배운 모든 것을 종합하여, 자신의 실제 업무에 적용할 워크플로우를 설계해보세요:

```text
내 업무에서 가장 자주 하는 작업 3가지를 골라서,
각각에 맞는 확장 기능(Skill, Command, Subagent 중)을 설계해줘.

각 항목에 대해 다음을 포함해줘:
1. 어떤 작업인지
2. 왜 이 확장 유형(Skill/Command/Subagent)을 선택했는지
3. SKILL.md 또는 Command 파일의 핵심 내용 (name, description, 역할)
4. 이 3개를 조합했을 때 전체 워크플로우가 어떻게 돌아가는지
```

- 결과를 검토하면서 "이건 Skill이 아니라 CLAUDE.md 규칙이 맞겠다" 같은 판단을 연습
- 설계가 마음에 들면 실제로 파일을 생성하여 테스트

---

## QUIZ

**문제:** 이 커리큘럼에서 배운 확장 기능의 계층 순서로 올바른 것은?

| 선택지 | 내용 |
|--------|------|
| A | CLAUDE.md → Skills → Hooks + MCP → Subagents → Agent Teams → Plugins |
| B | CLAUDE.md → Hooks + MCP → Skills → Subagents → Agent Teams → Plugins |
| C | CLAUDE.md → Skills → Subagents → Hooks + MCP → Agent Teams → Plugins |

**정답:** A — CLAUDE.md(기본 규칙)를 기반으로, Skills(자동 로딩 지식) → Hooks + MCP(자동화 + 외부 도구) → Subagents(독립 위임) → Agent Teams(병렬 협업) → Plugins(배포/패키징) 순서로 계층이 쌓인다. 아래에서 위로, 단순한 것에서 복잡한 것으로 확장해가는 구조다.
