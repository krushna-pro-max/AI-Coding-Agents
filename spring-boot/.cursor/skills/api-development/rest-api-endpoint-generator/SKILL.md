---
name: rest-api-endpoint-generator
description: Generates REST endpoints for Java/Spring Boot: controllers, request/response records, HTTP semantics. Use when adding or refactoring REST resources.
---

# REST API Endpoint Generator

## When to Apply

Use when adding or refactoring REST resources in Java/Spring Boot (Java 21, records, constructor injection).

## Rules

- **Resource-based**: One controller per resource; base path `@RequestMapping("/api/v1/{resource}")`.
- **Structure**: `@RestController`, `@RequiredArgsConstructor`, constructor-injected service(s). Return `ResponseEntity<T>`.
- **DTOs only**: Never expose entities. Records: `*Request` for body, `*Response` (or `*Dto`) for output. Map in service layer.
- **HTTP semantics**:
  - GET collection → 200 + list (or paged wrapper).
  - GET by id → 200 + body, or 404.
  - POST → 201 + body + `Location` header.
  - PUT/PATCH → 200 + body, or 404.
  - DELETE → 204 No Content, or 404.

## Output

Controller methods, request/response records, service method signatures. No business logic in controller—delegate to service.
