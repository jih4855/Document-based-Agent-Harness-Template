# 에이전트 위임 정책

이 파일은 **메인 에이전트가 작업을 어떻게 위임하는지**를 정의합니다. 런타임
카탈로그가 아닙니다. 사용 가능한 서브에이전트 목록은 사용하는 에이전트 도구가
관리합니다 (예: Claude Code의 `/agents`, Codex/Cursor의 동등한 명령).

이 파일은 짧게 유지합니다. 상세 런타임 프롬프트는 `context/runtime_agents/`,
재사용 가능한 작업 절차는 `skills/`에 둡니다.

## 메인 에이전트가 담당

- 전략, 선호, 문체, 품질 기준
- 반복 workflow를 스킬이나 서브에이전트로 분리할지 판단
- `context/tacit.md`, `context/memory.md`, skills, 이 정책 갱신
- 서브에이전트가 막힐 때 멘토링하거나 직접 인수

## 서브에이전트가 담당

- 문서화된 단일 업무
- 스킬 또는 런타임 템플릿 기반 반복 실행
- 좁은 파일 읽기와 scoped 변경
- 상태, 검증, blocker, 다음 행동 보고

## 절대 위임하지 않는 일

서브에이전트가 처리할 수 있어 보여도 메인이 직접 처리해야 하는 일:

- 사용자 대상 전략 또는 선호 변경
- `context/tacit.md`, skills, 이 정책의 변경
- 새로운 workflow 설계 결정
- 사용자 명시 승인 없는 파괴적·되돌리기 어려운 작업

## 공통 출력 계약

모든 서브에이전트는 아래 항목을 보고합니다.

`status`, `summary`, `actions_taken`, `files_read`, `files_changed`,
`recommended_next_steps`

서브에이전트의 런타임 템플릿이 자체 출력을 정의하더라도 이 계약을 대체할 수
없으며 확장만 할 수 있습니다.

## 도구별 디스커버리

런타임 에이전트 카탈로그는 이 파일이 아니라 활성 에이전트 도구가 소유합니다.
이 파일은 위임 정책을 다룹니다. `context/runtime_agents/`는 handoff template의
portable source of truth입니다.

- Claude Code에서는 프로젝트 subagent를 `.claude/agents/<name>.md`, 사용자 전역
  subagent를 `~/.claude/agents/<name>.md`에 둡니다. `/agents`로 생성, 검사, 관리할
  수 있습니다. frontmatter의 `description` 필드는 자동 위임 판단의 중요한 신호입니다.
- Codex에서는 지원되는 경우 `.codex/config.toml`과 `.codex/agents/<name>.toml` 같은
  프로젝트 Codex config에 도구 전용 reusable role을 mirror할 수 있습니다. portable
  handoff 지침은 `context/runtime_agents/<name>.md`에 두고, Codex 전용 role 파일은
  그 template을 다시 가리키게 합니다.
- 도구 중립 환경에서는 `context/runtime_agents/<name>.md`를 하니스의 source of truth로
  둡니다. 활성 런타임이 위임을 지원하면 호출 시점에 파일 내용을 서브에이전트
  프롬프트에 주입합니다. 위임을 지원하지 않으면 메인이 같은 파일을 실행 playbook으로
  사용할 수 있습니다.

## 에스컬레이션 규칙

서브에이전트가 맥락, 인증 정보, 권한, 판단 권한 부족으로 완료하지 못하면
blocker를 보고해야 합니다. 메인은 진단하고, handoff를 좁히거나, 직접 완료
합니다. 서브에이전트는 막힘을 풀려고 새 정책을 만들지 않습니다.
