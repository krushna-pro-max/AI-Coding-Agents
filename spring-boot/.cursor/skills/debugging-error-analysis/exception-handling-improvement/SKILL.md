---
name: exception-handling-improvement
description: Improves exception handling: avoid swallowing, map to HTTP/API errors, and use @ControllerAdvice. Use when reviewing or refactoring try/catch and error responses.
---

# Exception Handling Improvement

## When to Apply

Use when the user wants to improve how exceptions are handled: less swallowing, consistent API errors, or better mapping to HTTP status.

## Conventions (Java / Spring Boot)

- **Do not swallow**: Avoid empty `catch` blocks or logging without rethrow. Either handle (e.g. map to 404/400 response) or rethrow. Use `_` for unused exception variable (Java 21) only when intentionally ignoring.
- **Centralized API errors**: Use `@RestControllerAdvice` with `@ExceptionHandler` for domain and infrastructure exceptions. Return a consistent error body (e.g. `ErrorResponse` record) and appropriate status (400, 404, 409, 500).
- **Mapping**: Map specific exceptions (e.g. `ResourceNotFoundException` → 404, `ConstraintViolation` → 400, `DataIntegrityViolationException` → 409 or 400). Have one generic handler for unexpected exceptions (500) and log with context.
- **Layering**: Services throw domain or persistence exceptions; controllers do not catch for business cases—let the advice handle. Controllers may catch only for request-specific handling when necessary.

## Output

- List of current issues (swallowed exceptions, wrong status, duplicate handling).
- Suggested `@ExceptionHandler` methods and exception hierarchy (if needed).
- Before/after snippets for key spots; ensure logging with context before returning or rethrowing.
