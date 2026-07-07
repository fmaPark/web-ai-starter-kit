---
type: Module
title: Backend Architecture
description: <백엔드 아키텍처를 한 줄로 설명>
tags: [backend, architecture]
timestamp: <YYYY-MM-DDTHH:MM:SSZ>
---

<!-- 안내: 이 문서는 실제 코드에서 에이전트가 역생성합니다. 코드가 바뀌면 재역생성해야 정확합니다. -->

# Folder & Layer Structure

<!-- 안내: 백엔드 폴더 구조와 각 레이어(라우터/서비스/리포지토리 등)의 역할을 서술하세요. -->
<폴더/레이어 구조>

# Request Flow

<!-- 안내: 요청이 진입점부터 응답까지 어떤 순서로 처리되는지 서술하세요. -->
<요청 처리 흐름>

# Common Patterns

<!-- 안내: 프로젝트 전반에 반복되는 공통 패턴을 서술하세요. -->
- Dependency Injection: <...>
- Auth: <...>
- Error Handling: <...>
- Config: <...>

# Entry Points

<!-- 안내: 앱 진입점(ASGI app, main 등) 코드 링크. -->
- `../src/backend/<...>.py`

# Contract Note

<!-- 안내: 원칙(단일 정본, 복제 금지)은 고정입니다. 정본 아티팩트 이름만 프로젝트에 맞게 채우세요. -->
API 계약의 정본은 <정본 아티팩트, 기본: OpenAPI `/openapi.json`>이며, 그 정확도는
라우터/스키마 코드가 정본 아티팩트에 정확히 반영된다는 전제 위에 성립합니다.
라우터·스키마 변경 시 정본 아티팩트를 반드시 함께 갱신/확인하세요.
