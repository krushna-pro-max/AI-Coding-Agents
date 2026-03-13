---
name: input-validation-sanitization
description: Implements input validation and sanitization to prevent injection and XSS. Use when securing request data, query params, or user-generated content.
---

# Input Validation & Sanitization

## When to Apply

Use when the user needs to harden input handling: request bodies, path/query params, headers, or stored content that is later rendered.

## Conventions

- **Validation**: Use Bean Validation (`@Valid`, `@NotNull`, `@Size`, `@Pattern`, `@Email`, etc.) on all untrusted input. Reject invalid input with 400; handle in `@ControllerAdvice` (see API Error Handling skill).
- **Sanitization**: For string output (e.g. HTML, JSON), encode or sanitize to prevent XSS. Prefer context-aware encoding (e.g. HTML entity encoding for HTML body). Never trust client-supplied HTML/script without a strict allowlist.
- **Injection**: Use parameterized queries (JPQL with `:param`, JPA criteria, or prepared statements). Never concatenate user input into SQL or JPQL strings. Validate/sanitize file names and paths if handling file uploads.
- **Length and format**: Enforce max length and allowed character set where applicable (e.g. `@Size(max=...)`, `@Pattern`). Reject oversized payloads (configure max body size if needed).

## Output

- Request DTOs with validation annotations and, if needed, custom validators.
- Short guidance on encoding (e.g. OWASP Encoder, or framework defaults) and where to apply it (e.g. response DTOs, templates).
- Checklist: validate → sanitize/encode → use parameterized access.
