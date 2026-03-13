---
name: api-documentation-creator
description: Creates API documentation using OpenAPI 3 and Swagger (SpringDoc). Use when documenting REST endpoints, request/response schemas, or exposing Swagger UI.
---

# API Documentation Creator

## When to Apply

Use when the user needs to document REST APIs with **OpenAPI 3** and **Swagger** (e.g. SpringDoc in Java/Spring Boot).

## Tools

- **OpenAPI 3**: Machine-readable spec (YAML/JSON); use for codegen, tooling, and single source of truth.
- **Swagger UI**: Interactive UI to explore and try endpoints; typically served from the same app (e.g. `/swagger-ui.html` or `/swagger-ui/index.html` with SpringDoc).

## Conventions (SpringDoc / Spring Boot)

- Add `springdoc-openapi-starter-webmvc-ui` (or equivalent). Define an `OpenAPI` bean for API info, servers, and tags.
- **Controllers**: Use `@Operation(summary, description)`, `@Parameter` for path/query/header, `@ApiResponse` for status codes and response description.
- **DTOs**: Use `@Schema` on request/response records (description, example, required). Document error body (e.g. `ErrorResponse`) and reference it in `@ApiResponse`.
- **Tags**: Group endpoints by resource or domain (e.g. `@Tag(name = "Items")`). Document pagination params (`page`, `size`, `sort`) and filter params.

## Output

- OpenAPI config snippet (info, servers, tags).
- Example annotations on one controller and one request/response type.
- How to access the spec (`/v3/api-docs`) and Swagger UI; note any security (e.g. exclude from auth in dev).
