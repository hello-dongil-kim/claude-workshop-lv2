# Plugin 디렉토리 템플릿

아래 구조를 참고하여 자신의 Plugin 디렉토리를 구성하세요.
`{...}` 부분을 팀/조직에 맞게 채우면 됩니다.

---

## 기본 구조

```
{plugin-name}/
├── .claude-plugin/
│   └── plugin.json             # 플러그인 매니페스트 (이 폴더 안에만)
├── skills/                     # Skills 모음
│   └── {skill-name}/
│       ├── SKILL.md            # 스킬 정의
│       └── references/         # 참조 자료 (선택)
├── commands/                   # Commands 모음 (선택)
│   └── {command-name}.md
└── agents/                     # Subagents 모음 (선택)
    └── {agent-name}.md
```

> **위치 규칙:** 매니페스트인 `plugin.json`만 `.claude-plugin/` 폴더 안에 두고, `skills/`·`commands/`·`agents/` 등 나머지 디렉터리는 플러그인 **루트**에 둔다.

---

## .claude-plugin/plugin.json 템플릿

```json
{
  "name": "{plugin-name}",
  "description": "{플러그인이 하는 일을 한 줄로 요약}",
  "version": "0.1.0"
}
```

---

## 작성 가이드

### 1. 이름 (plugin-name)
- 영문 소문자, 하이픈(`-`)만 사용
- 팀/조직명을 접두어로: `{team}-{기능}` (예: `ux-team-research`, `pmo-governance`)
- 네임스페이스가 되므로 간결하게

### 2. 최소 구성
- Plugin은 **Skill 1개만으로도 성립**한다
- 처음에는 skills/ 하나로 시작하고, 필요할 때 commands/와 agents/를 추가

### 3. 네임스페이스 규칙
설치 후 스킬은 `{plugin-name}:{skill-name}` 형식으로 호출된다:
- `ux-team-research:interview-guide`
- `pmo-governance:launch-checklist`

---

## 기획자용 Plugin 아이디어

| Plugin 이름 | 포함 요소 | 대상 |
|------------|-----------|------|
| `ux-research` | 리서치 브리프 Skill + 인터뷰 가이드 Command + 인사이트 분석 Agent | UX 리서치 �� |
| `service-planning` | PRD 작성 Skill + 경쟁사 스캔 Command + 스펙 리뷰 Agent | 서비스 기획 팀 |
| `pmo-governance` | 출시 체크리스트 Skill + KPI 대시보드 Command + 품질 감사 Agent | PMO |
| `data-ops` | 데이터 정리 Skill + SQL 생성 Command | 데이터 분석 팀 |
