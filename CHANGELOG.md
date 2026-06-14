# Changelog

이 워크샵의 주요 변경 이력. 형식은 [Keep a Changelog](https://keepachangelog.com/) 기반. 시리즈 공통 표준은 제작자 내부 문서 `workshop-series-standard`를 따른다.

## [2026-06-14] — 9+ 품질 개선

### Added (추가)

- 모든 EXECUTE에 `✅ 이렇게 되면 성공` 성공 기준(P1)
- 각 블록 QUIZ에 적용형(시나리오) 문항 + 오답 이유 해설(P3)
- 진도 영속화·적응형 건너뛰기·오답 remediation 규칙과 루트 `progress.md`(P4)
- 버전 의존 정보용 변동 정보 박스(P2, 세션별 핵심 1~2곳)
- 작동하는 end-to-end 예제: 서브에이전트 생성→`@`호출→결과 확인, 스킬→플러그인 패키징→로컬 설치
- 안전 경고: MCP 프롬프트 인젝션·토큰 최소권한, Hook exit code 2 부작용, Plan Mode 보고 우선
- README 제작자 푸터, `LICENSE`(All rights reserved, 개인 학습 이용 허용), `.markdownlint.jsonc`

### Changed (변경)

- NAVER 조직 콘텐츠를 vendor-neutral로 일반화(내부 위키 URL·내부 이메일·사내 전용 도구명 제거)
- 무출처 정량 주장 완충, 용어("컨텍스트 오염")·난이도 표기 통일

### Fixed (수정)

- Hook 이벤트 `PostResponse`(없는 이벤트) → `Stop`
- Subagent 정의를 `.claude/agents/<name>.md` 단일 파일로 정정(폴더+SKILL.md 오표기 제거)
- Plugin 매니페스트를 `.claude-plugin/plugin.json`으로 정정
- MCP JSON `"type":"url"` → `"type":"http"`, 위치를 `.mcp.json`/`~/.claude.json`로 정정
- 깨진 `@templates/skill-template.md` 참조를 실존 경로로 복구
