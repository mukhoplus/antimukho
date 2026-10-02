# Antigravity 설정

이 디렉터리는 Antigravity Agent의 공통 동작 규칙과 모델 라우팅 설정을 관리합니다.

## 파일 구성

```text
.agents/
└── rules/
    └── prompts.md    # [공식 규칙 경로] Antigravity가 자동 인식하는 공통 행동 지침

.antigravity/
├── routing.yml       # 작업 유형별 권장 모델 및 사용자 전환 유도 규칙
└── README.md         # 설정 체계 안내 문서

AGENTS.md             # 프로젝트별 구체적 개발 규칙 (네이티브 자동 로드)
```

## 파일 역할

### `routing.yml`

작업의 성격과 복잡도에 따라 권장할 모델과 정책을 정의합니다.

> **IDE 동작 방식**: IDE 상에서 Agent는 실행 모델을 자체 전환할 수 없습니다. 따라서 Agent는 본 규칙을 기준으로 현재 작업이 고성능 추론이나 심화 디버깅이 필요할 경우, **답변 하단에 사용자에게 모델 전환을 권장(TIP 안내)**하도록 동작합니다.

주요 역할:

- 작업 유형 분류 (`simple`, `complex`, `critical_bug`)
- 권장 기본/Fallback 모델 지정
- 에스컬레이션 및 모델 전환 안내 기준 정의

### `.agents/rules/prompts.md`

Antigravity 시스템에 의해 자동으로 컨텍스트에 주입되는 공통 행동 규칙입니다.

주요 내용:

- 코드베이스 사전 분석
- 기존 구조와 규칙 준수
- 최소 범위 수정 및 스코프 제어
- 테스트 및 검증 철칙
- 오류 처리 및 보안
- 모델 전환 권장(Model Routing Guidance) 행동 지침

### `AGENTS.md`

개별 프로젝트에서만 적용되는 도메인/기술 규칙을 정의합니다. (Antigravity 자동 로드)

예:

- 프로젝트 기술 스택
- 디렉터리 구조 및 네이밍 규칙
- API/DB/Git 규칙
- 테스트 및 빌드 실행 명령

Global 규칙은 `.agents/rules/prompts.md`에 두고, 프로젝트별 규칙은 `AGENTS.md`에 정의합니다.

## 우선순위

설정 간 충돌이 발생할 경우 다음 순서로 프로젝트의 구체적인 규칙을 우선 적용합니다.

1. 사용자의 현재 작업 요청
2. 프로젝트의 `AGENTS.md`
3. `.agents/rules/prompts.md`
4. `.antigravity/routing.yml`

보안 및 시스템 수준의 제한은 위 규칙보다 우선합니다.

## 관리 원칙

- 실제 프로젝트에 필요한 규칙만 추가합니다.
- 동일한 규칙을 여러 파일에 중복해서 작성하지 않습니다.
- Global 규칙에는 특정 프로젝트에 종속된 내용을 넣지 않습니다.
- 모델 ID나 라우팅 정책을 변경할 경우 `routing.yml`만 수정합니다.
- 프로젝트별 개발 방식이 달라지는 경우 `AGENTS.md`에 정의합니다.
