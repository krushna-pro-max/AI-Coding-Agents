---
name: api-documentation-generator-openapi
description: Generates OpenAPI 3 documentation for Spring Boot with SpringDoc: @Operation, @Parameter, @Schema, ErrorResponse. Use when adding or improving API docs and Swagger UI.
---

# API Documentation Generator (OpenAPI)

## When to Apply

Use when adding or improving OpenAPI docs and Swagger UI for Spring Boot REST APIs.

## Rules

- **SpringDoc**: Use `springdoc-openapi-starter-webmvc-ui` (or equivalent). Group by tags (e.g. by resource).
- **Annotate**: `@Operation` (summary, description), `@Parameter` (path/query/header), `@ApiResponse`. `@Schema` on request/response records (description, example, required).
- **Errors**: Document 400, 404, 409, 500; reference same `ErrorResponse` schema.
- **Pagination/filtering**: Document `page`, `size`, `sort`, and filter params with `@Parameter` and `@Schema` (examples, defaults).

## Output

OpenAPI config (`OpenAPI` bean with info, servers, tags), example `@Operation`/`@Parameter`/`@Schema` on one controller and one DTO, and how to access `/v3/api-docs` and Swagger UI.
