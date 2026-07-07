---
type: Contract
title: <계약명>
description: <이 계약이 다루는 API 영역을 한 줄로 설명>
spec_ref: <정본 스키마 포인터, 예: /openapi.json#/paths/~1api~1<...>, schema.graphql#<Type>, ../src/backend/<...>.py>
tags: [<태그1>, <태그2>]
timestamp: <YYYY-MM-DDTHH:MM:SSZ>
---

# Source of Truth

<!-- 안내: 이 섹션의 원칙은 고정입니다. 요청/응답 스키마를 이 문서에 복제하지 마세요.
     엔드포인트 목록만 나열하고, 상세 스키마는 spec_ref(정본 아티팩트)를 참조합니다. -->
스키마 정본은 <정본 아티팩트, 기본: OpenAPI `/openapi.json`>입니다. 이 문서는 스키마를 복제하지 않습니다.

## Endpoints

- `<METHOD> <경로>` — <한 줄 설명>

# Behavioral Notes

<!-- 안내: OpenAPI 스펙에 담기지 않는 규약을 **사람이** 작성하세요.
     예: 인증 요구사항, 상태코드별 의미, 부수효과(사이드이펙트), 멱등성, 레이트리밋. -->
- 인증: <...>
- 상태 코드: <...>
- 부수효과: <...>

# Related

<!-- 안내: 이 계약을 구현하는 코드를 링크하세요. -->
- Backend: `../src/backend/<...>.py`
- Frontend caller: `../src/frontend/<...>.tsx`
