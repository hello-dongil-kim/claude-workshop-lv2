# Block 2: MCP + Hooks 실습

## EXPLAIN

### 오늘 할 것

| 실습 | 내용 | 시간 |
|------|------|------|
| MCP 서버 연결 | 자주 쓰는 도구 1개를 Claude에 연결 | ~5분 |
| Hook 설정 | 간단한 자동화 Hook 1개 설정 | ~5분 |

### MCP 연결 순서

1. **도구 선택** — 가장 자주 쓰는 것부터 (Notion 추천)
2. **연결 명령어 실행** — `claude mcp add --transport http [이름] [URL]`
3. **확인** — `/mcp`로 연결 상태 확인
4. **테스트** — 간단한 요청으로 작동 확인

### 주요 MCP 서버 연결 명령어

| 서버 | 방법 | 명령어/절차 |
|------|------|------------|
| **Notion** | CLI | `claude mcp add --transport http notion https://mcp.notion.com/mcp` |
| **Slack** | Connectors | 아래 절차 참고 |
| **Gmail** | Connectors | Slack과 동일한 절차 (Gmail 선택) |

**Slack/Gmail 연결 절차 (Connectors 방식):**

1. [claude.ai](https://claude.ai) 접속 → 좌측 하단 프로필 → **Settings**
2. **Connectors** 탭 클릭
3. 원하는 서비스(Slack, Gmail 등) 옆 **Connect** 클릭
4. OAuth 인증 화면에서 **Allow** → 연결 완료
5. Claude Code(터미널/IDE)에서 `/mcp`로 연결 상태 확인

> **참고:** Connectors로 연결한 서버는 claude.ai 계정에 연동되므로, 같은 계정이면 터미널과 IDE 모두에서 자동으로 사용 가능하다.

### Hook 설정 순서

1. Claude에게 Hook 설정 요청
2. settings.json에 자동 추가됨
3. 테스트로 동작 확인

### 자주 발생하는 문제와 해결법

| 증상 | 원인 | 해결 |
| ---- | ---- | ---- |
| `/mcp`에 서버가 안 보임 | CLI 명령어 오타 또는 URL 오류 | `claude mcp list`로 등록 상태 확인. 안 되면 삭제 후 재등록 |
| MCP 연결은 됐는데 요청이 실패 | OAuth 인증 만료 또는 권한 부족 | claude.ai Settings → Connectors에서 Disconnect → 재연결 |
| Hook이 실행되지 않음 | matcher 값이 실제 도구명과 불일치 | `Write`, `Edit`, `Read` 등 정확한 도구명 사용. 대소문자 구분 |
| Hook 실행 시 에러 발생 | 쉘 스크립트 구문 오류 | 터미널에서 command 부분만 직접 실행하여 오류 확인 |

**안 되면 이것부터 확인 — 디버깅 3단계:**

```text
1단계: Claude에게 물어보기
  "방금 설정한 MCP 서버(또는 Hook)가 작동하지 않아.
   settings.json을 확인하고 문제를 찾아줘."
  → 대부분 여기서 해결됨

2단계: 설정 파일 직접 확인 요청
  ".claude/settings.json 내용을 보여줘."
  → Claude가 읽고 오류를 지적해줌

3단계: 초기화 후 재설정
  "이 Hook(또는 MCP)을 삭제하고 처음부터 다시 설정해줘."
  → 꼬인 설정을 깨끗하게 재시작
```

> **핵심: 디버깅도 Claude에게 시키면 된다.** 직접 JSON을 읽을 필요 없다.

---

## EXECUTE

다음을 직접 실행해보세요:

**Step 1: MCP 서버 연결**
- 아래 중 하나를 선택해서 실행:

옵션 A (Notion — CLI):
```
claude mcp add --transport http notion https://mcp.notion.com/mcp
```

옵션 B (Slack/Gmail — Connectors):
```
claude.ai → Settings → Connectors → 원하는 서비스 Connect 클릭
```

옵션 C (다른 서버):
```
내가 자주 쓰는 도구를 MCP로 연결하고 싶어. 추천해줘.
```

**Step 2: 연결 확인 및 테스트**
```
/mcp
```
연결된 서버가 보이면, 간단한 테스트 요청:
```
Notion에서 최근 수정한 페이지 3개를 보여줘
```

**Step 3: Claude에게 Hook 설정 시키기**

```text
파일을 생성할 때마다 현재 시간을 터미널에 출력하는 Hook을 설정해줘.
설정 완료 후, 제대로 작동하는지 테스트 파일을 하나 만들어서 확인해줘.
```

- Claude가 settings.json에 Hook을 추가하고, 테스트까지 해줌
- **핵심: Hook의 JSON 문법을 직접 쓸 필요 없다. Claude에게 "이런 자동화를 걸어줘"라고 말하면 된다**
- 결과가 기대와 다르면: "matcher를 Write 대신 Edit으로 바꿔줘" 등 수정 지시

---

## QUIZ

**문제:** Notion에서 데이터를 가져와 파일로 저장할 때, 자동 백업도 하고 싶다면?

| 선택지 | 내용 |
|--------|------|
| A | MCP로 Notion을 연결하고, Hook으로 파일 저장 시 자동 백업 |
| B | Hook으로 Notion을 연결하고, MCP로 백업 설정 |
| C | MCP 서버 설정에서 자동 백업 옵션을 활성화 |

**정답:** A — MCP는 외부 도구 연결(Notion 접근), Hook은 작업 전후 자동 실행(파일 저장 시 백업). 역할이 분리되어 있다. "어디에 접근할 것인가"는 MCP, "자동으로 뭘 할 것인가"는 Hook이다.
