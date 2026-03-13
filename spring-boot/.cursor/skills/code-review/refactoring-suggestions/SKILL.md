---
name: refactoring-suggestions
description: Suggests refactorings to improve structure without changing behavior: extract method, rename, introduce DTO, split class. Use when improving existing code.
---

# Refactoring Suggestions

## When to Apply

Use when the user wants concrete refactoring ideas to improve code structure, readability, or alignment with standards (Java/Spring Boot).

## Process

1. **Scope**: Prefer small, safe steps (extract method, rename, move) over large rewrites unless the user asks for it.
2. **Behavior-preserving**: Refactorings should not change observable behavior; suggest tests to run before/after.
3. **Project alignment**: Prefer records for DTOs, constructor injection, thin controllers, DTOs at API boundary, and centralized error handling.

## Common Suggestions

- **Extract method**: Long method → break into named private methods or move to service.
- **Introduce DTO**: Controller returning entity → add `*Response` record and map in service.
- **Rename**: Unclear name → suggest clearer name (camelCase, *Controller/*Service/*Request/*Response).
- **Split class**: Class with multiple responsibilities → suggest separate classes by concern.
- **Replace with pattern**: Verbose null/optional handling → `orElseThrow()`, pattern matching for instanceof.

## Output

- Ordered list of refactorings (quick wins first).
- For each: current code location, suggested change in one sentence, optional before/after snippet.
- Note any tests or verification step to run.
