# docs — 지식 레이어 사용 가이드

이 폴더는 OKF(Open Knowledge Format) 기반 프로젝트 지식베이스입니다.
코드 레포의 `docs/`에 submodule로 마운트되는 것을 전제로 하며,
문서 안의 코드 링크는 `../src/...` 상대경로를 사용합니다.

## 폴더 역할과 작성 주체

| 폴더/파일 | 역할 | 작성 주체 |
|-----------|------|-----------|
| `index.md` | okf_version 선언 + 전체 목차 + 정본 원칙 | 사람 (초기 1회) |
| `overview.md` | 시스템 개요 (목적/기능 영역/스택/구조) | 사람 + 에이전트 보조 |
| `log.md` | 지식베이스 변경 이력 | 변경한 주체가 기록 |
| `features/` | 기능 정의 (**정본**) | **사람** — 기획 엑셀에서 수기 이관, 자동생성 금지 |
| `backend/` | 백엔드 구조/모델 | **에이전트** — 코드에서 역생성 |
| `frontend/` | 프론트 구조/컴포넌트/페이지 | **에이전트** — 코드에서 역생성 |
| `contracts/` | API 계약 참조 (스키마 정본은 OpenAPI) | 에이전트 역생성 + 사람(Behavioral Notes) |
| `domains/` | 도메인 단위 책임/경계 (기능이 많아지면) | 사람 |
| `decisions/` | ADR — 설계 결정 이력 (비정본) | 사람 |

## 새 문서 만드는 규칙

1. 해당 폴더의 `_TEMPLATE.md`를 복사해 새 파일을 만든다.
   (예: `features/_TEMPLATE.md` → `features/<기능-슬러그>.md`)
2. frontmatter의 자리표시자(`<...>`)를 실제 값으로 채운다.
3. 본문의 `<!-- 안내: ... -->` 주석을 읽고 각 섹션을 작성한 뒤, 안내 주석은 지워도 된다.
4. 해당 폴더의 `index.md` 목차에 새 문서를 추가한다.
5. `log.md`에 변경 이력을 남긴다.

## frontmatter 규칙 요약

- 모든 concept 문서(.md)는 YAML frontmatter로 시작하며 **`type` 필드는 필수**.
- 허용 필드: `type`, `title`, `description`, `tags`, `timestamp` + 파일별 지정 필드
  (예: Feature의 `status`/`owner`/`spec_source`/`spec_synced_at`, Contract의 `spec_ref`).
- `index.md`와 `log.md`는 예약 파일이라 frontmatter 없음.
  단 `docs/index.md`만 예외로 `okf_version: "0.1"`을 가진다.
- 섹션 헤더는 템플릿의 영문 고정어를 그대로 사용한다(파싱 안정성).

## 채우는 권장 순서

1. **씨앗 3파일**: `index.md` → `overview.md` → `log.md`
2. **역생성**: `backend/` → `frontend/` → `contracts/` (실제 코드 기준으로 에이전트가 생성)
3. **수기 이관**: `features/` (기획 엑셀에서 사람이 이관)

## 정본 원칙

- API 스키마의 정본은 **OpenAPI(`/openapi.json`)**. 문서에 스키마를 복제하지 않는다.
- 기능 정의의 정본은 **`features/` 수기 문서**. 자동생성하지 않는다.
- 코드 구조 문서는 **역생성 산출물**. 코드가 바뀌면 다시 역생성해야 정확하다.
