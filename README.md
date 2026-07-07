# web-ai-starter-kit

**코드는 남지만, 맥락은 증발합니다.**

왜 그렇게 만들었는지, 기획과 코드가 어디서 어긋났는지, 어떤 컴포넌트를 재사용할 수 있는지 —
사람도 AI 에이전트도 이것을 모르면 매번 코드베이스 전체를 처음부터 다시 읽어야 합니다.

이 키트는 그 맥락이 **처음부터 쌓이는 구조**로 프로젝트를 시작하게 해주는
**지식 + AI 스타터 키트**입니다. client + API 형태의 웹개발 프로젝트라면 스택과 무관하게
복제해 쓸 수 있으며, 템플릿 내 예시는 React/TypeScript/Next.js + FastAPI/Python 기준으로
작성되어 있습니다.

## 3레이어 개념

| 레이어 | 위치 | 역할 |
|--------|------|------|
| 지식 (Knowledge) | `docs/` | OKF(Open Knowledge Format) 기반 프로젝트 지식베이스. 기능 정의, 코드 구조, API 계약, 결정 기록 |
| 지시 (Instruction) | `skills/` (ai-skills) | 에이전트에게 주는 프로젝트별 지시 |
| 반복 절차 (Procedure) | `skills/` (ai-skills) | 반복 작업의 절차화(스킬) |

> `skills/`는 현재 자리만 잡혀 있습니다. 별도의 **ai-skills 레포**에서 채워질 예정이며,
> 새 프로젝트에서는 submodule로 마운트합니다.

## 사용법

### 1. 새 프로젝트에 붙이기

유일한 고정 제약은 하나입니다: **docs가 코드 레포 루트의 `docs/`에 위치해야 합니다.**
docs 안의 코드 링크가 `../src/...` 상대경로를 쓰기 때문이며, 이 조건만 지키면
submodule이든 일반 폴더든 상관없습니다.

**패턴 A — 키트를 코드베이스의 출발점으로 (권장, 단순)**

이 레포를 template으로 복제해 새 프로젝트 레포를 만들고, `docs/`는 일반 폴더로
코드 레포에 그대로 포함합니다. skills만 공유 submodule로 교체합니다.

```bash
# 키트를 복제해 새 프로젝트 레포로 시작한 뒤
git rm -r skills && git submodule add <ai-skills-repo-url> skills
```

**패턴 B — docs를 독립 레포로 분리**

docs를 코드 레포와 독립적으로 백업/버전관리하고 싶을 때만 선택합니다.

```bash
# 코드 레포 루트에서
git submodule add <docs-repo-url> docs
git submodule add <ai-skills-repo-url> skills
```

> 주의: docs와 skills는 라이프사이클이 다릅니다. docs는 **프로젝트별** 지식이고
> skills는 **프로젝트 간 공유** 자산이므로, 둘을 하나의 submodule로 묶으면
> 특정 프로젝트의 docs 커밋이 공유 레포에 섞입니다. 묶지 마세요.
> 또한 키트 전체를 `<repo>/kit/` 같은 하위 경로에 마운트하면 코드 링크가
> `../../src/...`로 깊어지므로 루트 `docs/` 배치를 유지하세요.

### 2. docs 채우는 순서

1. **씨앗 3파일**: `docs/index.md`(목적/목차) → `docs/overview.md`(시스템 개요) → `docs/log.md`(초기 엔트리)
2. **역생성**: `docs/backend/`, `docs/frontend/`, `docs/contracts/` — 실제 코드에서 에이전트가 역생성
3. **수기 이관**: `docs/features/` — 기획 엑셀에서 `_TEMPLATE.md`를 복사해 사람이 이관
4. 필요 시 `docs/domains/`(도메인 정리), `docs/decisions/`(ADR) 추가

자세한 규칙은 [docs/README.md](docs/README.md)를 보세요.

### 3. 정본 원칙 (Source of Truth)

- **API 계약 = 단일 기계가독 스키마 아티팩트**. 어떤 문서에도 스키마를 복제하지 않습니다.
  프로젝트 시작 시 아래 우선순위로 정본을 하나 지정하고 `docs/contracts/`는 포인터만 둡니다.
  1. 프레임워크가 자동 생성하는 OpenAPI(`/openapi.json`) — FastAPI, NestJS, Spring 등 (기본값)
  2. 자동 생성이 없으면 수기 `openapi.yaml`(spec-first)을 레포에 두고 정본으로 지정
  3. 프로토콜이 다르면 해당 스키마: GraphQL → SDL, gRPC → `.proto`, tRPC → 라우터 타입
  4. 어느 것도 없으면 코드의 스키마 정의(Pydantic/zod 등)를 정본으로 지정 —
     이 경우에도 문서로 스키마를 복제하지 않고 코드 파일을 포인터로 참조
- **기능 정의 = `docs/features/` 수기 작성**. 기획 원본(엑셀)에서 사람이 이관하며 자동 생성하지 않습니다.
- **코드 구조 = 역생성**. `docs/backend/`, `docs/frontend/`, `docs/contracts/`는 코드에서
  에이전트가 역생성하며, 코드 변경 시 다시 역생성해야 정확합니다.
