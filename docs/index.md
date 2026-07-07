---
okf_version: "0.1"
---

# Knowledge Base

<!-- 안내: 이 지식베이스가 어떤 프로젝트의 지식 레이어인지, 누가 왜 사용하는지 한 문단으로 쓰세요. -->
<지식베이스 목적 한 문단>

## Categories

- **[Features](features/index.md)** — 기능 단위 정의. 기획(엑셀)에서 사람이 수기로 이관하는 정본.
- **[Backend](backend/index.md)** — 백엔드 구조/모델. 코드에서 에이전트가 역생성.
- **[Frontend](frontend/index.md)** — 프론트엔드 구조/컴포넌트/페이지. 코드에서 에이전트가 역생성.
- **[Contracts](contracts/index.md)** — API 계약 참조. 스키마 정본은 OpenAPI.
- **[Domains](domains/index.md)** — 도메인 단위 책임/경계 정리.
- **[Decisions](decisions/index.md)** — 설계 결정 기록(ADR). 비정본(이력).
- **[Change Log](log.md)** — 지식베이스 변경 이력.

## Source of Truth

<!-- 안내: 아래 원칙은 고정입니다. 프로젝트마다 수정하지 마세요. -->
- **API 스키마 정본 = OpenAPI(`/openapi.json`)**. 어떤 문서에도 스키마를 복제하지 않는다.
- **기능 정의 정본 = `features/` 수기 문서**. 기획 원본에서 사람이 이관하며 자동생성하지 않는다.
- 코드 구조 문서(backend/frontend/contracts)는 코드에서 역생성하며, 코드 변경 시 재역생성한다.
