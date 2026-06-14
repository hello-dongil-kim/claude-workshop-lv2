# Hook 설정 템플릿

아래 템플릿을 참고하여 settings.json에 Hook을 추가하세요.
`{...}` 부분을 자신의 업무에 맞게 채우면 됩니다.

---

## 템플릿

```json
{
  "hooks": {
    "{실행 시점}": [
      {
        "matcher": "{대상 도구}",
        "hooks": [
          {
            "type": "command",
            "command": "{실행할 쉘 명령어}"
          }
        ]
      }
    ]
  }
}
```

---

## 작성 가이드

### 1. 실행 시점 (4가지)

| 시점 | 언제 실행 | 기획자 활용 예시 |
|------|-----------|-----------------|
| `PreToolUse` | 도구 실행 **직전** | 중요 파일 삭제 차단, 경고 알림 |
| `PostToolUse` | 도구 실행 **직후** | 산출물 백업, 포맷 검증 |
| `PreCompact` | 컨텍스트 압축 **직전** | 핵심 맥락 보존 메모 |
| `Stop` | Claude가 응답을 마쳤을 때 | 작업 로그 기록, 알림 전송 |

### 2. matcher (대상 도구)

| matcher 값 | 의미 |
|------------|------|
| `Write` | 파일 생성 시 |
| `Edit` | 파일 수정 시 |
| `Read` | 파일 읽기 시 |
| `Bash` | 터미널 명령 실행 시 |

### 3. command (쉘 명령어)

> **참고:** Hook은 도구 실행 정보를 **stdin의 JSON 데이터**로 전달받는다. 복잡한 파싱이 필요한 경우 `jq` 등을 사용할 수 있지만, 대부분의 경우 **Claude에게 "이런 자동화 Hook 설정해줘"라고 요청하면 알아서 작성해준다.** JSON 문법을 직접 쓸 필요 없다.

---

## 기획자용 Hook 예시

> **핵심:** 아래 예시는 참고용이다. 실제로는 Claude에게 원하는 자동화를 자연어로 설명하면 settings.json에 자동 추가해준다.

### 파일 생성 알림

파일을 만들 때마다 터미널에 확인 메시지 출력:

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Write",
        "hooks": [
          {
            "type": "command",
            "command": "echo '[Hook] 파일이 생성되었습니다'"
          }
        ]
      }
    ]
  }
}
```

### 산출물 자동 백업

파일 생성 시 `./backups/` 폴더에 타임스탬프와 함께 복사본 생성:

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Write",
        "hooks": [
          {
            "type": "command",
            "command": "mkdir -p ./backups && cp \"$(cat /dev/stdin | jq -r '.tool_input.file_path')\" ./backups/$(date +%Y%m%d_%H%M%S)_backup"
          }
        ]
      }
    ]
  }
}
```

### 파일 수정 로깅

파일이 수정될 때마다 로그 기록:

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Edit|Write",
        "hooks": [
          {
            "type": "command",
            "command": "echo \"[$(date '+%H:%M:%S')] 파일 변경됨\" >> ./change-log.txt"
          }
        ]
      }
    ]
  }
}
```
