# 문서 기반 에이전트 하네스 템플릿

> 코딩 에이전트, workflow 에이전트, 장기 개인 자동화 프로젝트를 위한
> 가벼운 Markdown 하네스.

[![Template](https://img.shields.io/badge/type-template-111827)](#빠른-시작)
[![Markdown](https://img.shields.io/badge/built_with-Markdown-2563eb)](#폴더-구조)
[![Language](https://img.shields.io/badge/language-EN%20%2F%20KO-16a34a)](#영문판)

이 저장소는 **문서 우선 에이전트 하네스**입니다. 앱, 패키지, CLI, SDK를 포함하지
않습니다. 대신 에이전트에게 맥락, 작업 상태, 지속 암묵지, 재사용 스킬을 위한
명확한 Markdown 파일 묶음을 제공합니다.

커스텀 런타임을 만들지 않고도 에이전트가 매 세션 일관되게 동작하길 원할 때
사용합니다.

## 이 템플릿이 존재하는 이유

LLM 에이전트는 운영 규칙이 명시되어 있을 때 더 잘 작동합니다. 짧은 프롬프트는
잃기 쉽습니다. 문서화된 워크스페이스는 검사, 재사용, 개선이 쉽습니다.

이 템플릿은 작은 제어 레이어를 제공합니다.

| 레이어 | 파일 | 목적 |
| --- | --- | --- |
| 루트 계약 | `agent.md` | 에이전트가 무엇을 읽고 어떻게 일해야 하는지 |
| 암묵지 | `context/tacit.md` | 지속 규칙, 선호, 교훈, 인덱스 |
| 위임 라우터 | `context/agent_index.md` | 메인이 직접 할 일과 위임할 일의 정책 |
| 세션 메모리 | `context/memory.example.md` | 세션 간 프로젝트 메모리 예시 |
| 작업 상태 | `context/task.example.md` | 활성 작업과 결정 예시 |
| 스킬 인덱스 | `skills/index.md` | 스킬 카탈로그, 작성 규칙, 서브에이전트 메모 |

## 폴더 구조

```text
.
├── README.md
├── agent.md
├── .gitignore
├── context/
│   ├── tacit.md
│   ├── agent_index.md
│   ├── runtime_agents/
│   │   └── README.md
│   ├── memory.example.md
│   └── task.example.md
├── skills/
│   └── index.md
└── ko/
    ├── README.md
    ├── agent.md
    ├── .gitignore
    ├── context/
    │   ├── tacit.md
    │   ├── agent_index.md
    │   ├── runtime_agents/
    │   │   └── README.md
    │   ├── memory.example.md
    │   └── task.example.md
    └── skills/
        └── index.md
```

## 빠른 시작

예시 파일에서 live 상태 파일을 만듭니다.

```bash
cp context/memory.example.md context/memory.md
cp context/task.example.md context/task.md
```

그다음 사용하는 에이전트 도구로 저장소를 열고 에이전트에게 지시합니다.

```text
먼저 agent.md를 읽고, 거기 적힌 필수 읽기 순서를 따라줘.
```

이후:

1. 프로젝트 전용 운영 규칙은 `context/tacit.md`에 추가합니다.
2. 반복 위임 규칙은 `context/agent_index.md`에 추가합니다.
3. 활성 작업은 `context/task.md`에서 추적합니다.
4. 지속 결정은 `context/memory.md`에 기록합니다.
5. 반복 workflow는 `skills/` 아래에 추가합니다.
6. 스킬이 바뀌면 `skills/index.md`를 갱신합니다.

## 거버넌스 모델

거버넌스와 사용자 응대 판단은 메인 에이전트가 담당합니다.

- 사용자와 전략, 선호, 문체, 운영 기준 조율
- 새 workflow를 스킬로 만들지 서브에이전트로 만들지 판단
- tacit, skills, 위임 인덱스 갱신
- 위임된 에이전트가 막히면 멘토링하거나 인수

서브에이전트는 런타임 실행자 역할을 합니다.

- 위임받은 단일 업무 처리
- 문서화된 스킬과 런타임 템플릿 따름
- 변경 파일, 검증, blocker, 권장 다음 행동 보고
- 새 정책이나 선호 규칙은 메인에 라우팅하지 않고는 만들지 않음

요약: 메인은 사용자와 함께 규칙을 바꾸고, 서브에이전트는 문서화된 일을 반복합니다.

## 핵심 규칙

- `agent.md`를 루트 운영 계약으로 유지합니다.
- `context/tacit.md`를 현재 암묵지 인덱스로 유지합니다.
- `context/agent_index.md`를 현재 위임 정책으로 유지합니다.
- `skills/index.md`를 현재 스킬 인덱스로 유지합니다.
- live private 상태는 `context/memory.md`와 `context/task.md`에 둡니다.
- 비밀키, 토큰, 개인 일정, 고객 데이터, 로컬 인증 정보는 커밋하지 않습니다.
- 스킬과 서브에이전트는 사용자의 실제 워크플로우에 맞춰 구성합니다. 이 템플릿은
  구조만 제공합니다.

## 권장 스킬 구조

실제 스킬을 추가할 때는 아래 형태를 권장합니다.

```text
skills/
└── my-skill/
    └── SKILL.md
```

각 스킬에는 다음을 기술합니다.

- 사용 시점
- 필요한 입력
- 단계별 workflow
- 검증 절차
- 실패 대응
- 선택적 서브에이전트 위임 규칙

## 도구별 참고

에이전트 도구마다 프로젝트 지침을 읽는 방식이 다릅니다.

| 도구 동작 | 권장 설정 |
| --- | --- |
| `AGENTS.md` 자동 로드 | `agent.md`를 `AGENTS.md`로 복사하거나 심볼릭 링크 |
| `CLAUDE.md` 자동 로드 | `agent.md`를 `CLAUDE.md`로 복사하거나 심볼릭 링크 |
| 커스텀 스킬 지원 | `skills/`를 해당 도구의 스킬 폴더 규칙에 맞게 변환 |
| 자동 로드 미지원 | 에이전트에게 명시적으로 `agent.md`를 먼저 읽으라고 지시 |

이 템플릿은 도구 중립을 의도적으로 유지합니다.

## 영문판

같은 템플릿의 영어 버전이 저장소 루트에 있습니다.

영어 전용 저장소를 만들려면 루트 콘텐츠를 그대로 사용하면 됩니다.

## 이 템플릿이 아닌 것

이 저장소는 다음이 **아닙니다**.

- npm 패키지
- 에이전트 SDK
- 호스팅 런타임
- 프롬프트 모음
- 도구별 문서를 대체하는 자료

이 템플릿은 파일을 읽고 지침을 따르고 도구를 사용할 줄 아는 에이전트를 위한
최소 워크스페이스 계약입니다.
