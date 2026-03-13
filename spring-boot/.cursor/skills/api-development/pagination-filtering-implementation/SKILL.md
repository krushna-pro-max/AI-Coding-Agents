---
name: pagination-filtering-implementation
description: Implements pagination and filtering for REST list endpoints in Spring Boot (Pageable, PagedResponse, sort, filter params). Use when adding list APIs with paging or filters.
---

# Pagination & Filtering Implementation

## When to Apply

Use when adding or refactoring list endpoints that need pagination or filtering in Spring Boot.

## Rules

- **Pagination**: Spring `Pageable` and `Page`. `@RequestParam`: `page` (0-based), `size`, optional `sort` (e.g. `sort=name,asc`). Return a consistent wrapper, e.g. `record PagedResponse<T>(List<T> content, int page, int size, long totalElements, int totalPages)`.
- **Filtering**: Filter DTO or explicit `@RequestParam` (e.g. `status`, `fromDate`, `toDate`, `search`). Keep names stable and documented.
- **Sorting**: `sort` as comma-separated `property,direction`. Validate sort fields against an allowed list in service/repository.

## Output

Controller method with `Pageable` and filter params, `PagedResponse` record, service/repository usage, and note on default/max page size (config or constant).
