---
name: api-validation-middleware-creator
description: Creates API validation with Bean Validation and custom validators for Java/Spring Boot. Use when adding or standardizing request validation.
---

# API Validation Middleware Creator

## When to Apply

Use when adding or standardizing request validation (body, params, path variables) in Spring Boot.

## Rules

- **Bean Validation**: `@Valid` (or `@Validated`) on request bodies; use `jakarta.validation`: `@NotNull`, `@NotBlank`, `@Size`, `@Min`, `@Max`, `@Email`, `@Pattern`, `@Past`/`@Future`, etc.
- **Custom validators**: `@Constraint` + `ConstraintValidator` for cross-field or domain rules (e.g. date range). Keep validators reusable and unit-testable.
- **Method-level**: `@Validated` on controller and `@Valid` on `@RequestParam`/`@PathVariable` where needed (e.g. `@Min(1)` for id).
- **Error handling**: Validation failures handled in `@ControllerAdvice`; return 400 with consistent error payload. Use `MethodArgumentNotValidException` for body validation.

## Output

Request record with validation annotations, optional custom validator classes, and `@ControllerAdvice` snippet for validation exceptions.
