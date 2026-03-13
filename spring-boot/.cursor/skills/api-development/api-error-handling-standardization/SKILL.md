---
name: api-error-handling-standardization
description: Standardizes API error handling with @RestControllerAdvice and a single ErrorResponse shape in Java/Spring Boot. Use when centralizing or refactoring error responses.
---

# API Error Handling Standardization

## When to Apply

Use when centralizing error handling or defining a consistent API error format in Spring Boot.

## Rules

- **Centralized**: `@RestControllerAdvice` with `@ExceptionHandler`. Do not catch exceptions in controllers to return error JSON.
- **Error response**: Single record, e.g. `record ErrorResponse(String message, String code, int status, List<FieldError> errors, String path, Instant timestamp)`. Include `path` and `timestamp`.
- **Status codes**: 400 (validation, bad input), 404 (missing resource), 409 (e.g. duplicate), 500 (unexpected). Log with context before building response.
- **Validation errors**: For `MethodArgumentNotValidException`, return 400 and map `BindingResult.getFieldErrors()` to field/path + message + rejected value.

## Output

`ErrorResponse` record, `@RestControllerAdvice` with handlers for validation, `ResourceNotFoundException`, and optionally a generic handler. No swallowed exceptions.
