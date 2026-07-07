# web-starter-kit

웹개발(React/TypeScript/Next.js + FastAPI/Python) 프로젝트 착수 시 복제해 쓰는
**지식 + AI 스타터 키트**입니다. 특정 프로젝트에 종속되지 않는 템플릿 모음이며,
새 프로젝트를 시작할 때마다 이 레포를 출발점으로 삼습니다.

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

이 키트의 `docs/`와 `skills/`는 각각 독립 레포(또는 이 레포의 복제본)로 만들어
코드 레포에 submodule로 마운트하는 것을 전제로 합니다.

```bash
# 코드 레포 루트에서
git submodule add <docs-repo-url> docs
git submodule add <ai-skills-repo-url> skills
```

- `docs/`가 코드 레포의 `docs/`에 마운트되므로, docs 안의 코드 링크는
  `../src/...` 형태의 상대경로로 코드를 참조합니다.
- 프로젝트별 지식은 docs 레포에 쌓이고, 코드 레포와 독립적으로 백업/버전관리됩니다.

### 2. docs 채우는 순서

1. **씨앗 3파일**: `docs/index.md`(목적/목차) → `docs/overview.md`(시스템 개요) → `docs/log.md`(초기 엔트리)
2. **역생성**: `docs/backend/`, `docs/frontend/`, `docs/contracts/` — 실제 코드에서 에이전트가 역생성
3. **수기 이관**: `docs/features/` — 기획 엑셀에서 `_TEMPLATE.md`를 복사해 사람이 이관
4. 필요 시 `docs/domains/`(도메인 정리), `docs/decisions/`(ADR) 추가

자세한 규칙은 [docs/README.md](docs/README.md)를 보세요.

### 3. 정본 원칙 (Source of Truth)

- **API 스키마 = OpenAPI(`/openapi.json`)**. 어떤 문서에도 스키마를 복제하지 않습니다.
- **기능 정의 = `docs/features/` 수기 작성**. 기획 원본(엑셀)에서 사람이 이관하며 자동 생성하지 않습니다.
- **코드 구조 = 역생성**. `docs/backend/`, `docs/frontend/`, `docs/contracts/`는 코드에서
  에이전트가 역생성하며, 코드 변경 시 다시 역생성해야 정확합니다.
