---
name: anti-pattern-detection
description: Detects common anti-patterns in Java/Spring code: god classes, anemic models, leaky abstractions, and layer violations. Use when reviewing or refactoring code structure.
---

# Anti-Pattern Detection

## When to Apply

Use when the user wants to identify structural anti-patterns or bad habits in the codebase (Java/Spring Boot).

## Patterns to Flag

- **God class / long method**: Class or method doing too much; suggest split by responsibility or extract methods.
- **Anemic domain**: Entities as data bags with logic in services only; consider moving invariant logic into domain where it fits.
- **Leaky abstraction**: Lower-layer details (e.g. SQL, HTTP status) leaking into higher layers (e.g. domain); suggest encapsulate or map at boundary.
- **Layer violations**: Controller with business logic; repository with validation; domain depending on infrastructure. Enforce dependency direction (e.g. Clean Architecture).
- **Swallowed exceptions**: Empty catch or catch-that-only-logs without rethrow or proper handling. Flag and suggest `@ControllerAdvice` or rethrow.
- **Exposed entities**: Controllers returning JPA entities; suggest DTOs and mapping in service.

## Output

- List of detected anti-patterns with location (class/method) and short explanation.
- One concrete suggestion per finding (e.g. "Move validation to service", "Return ItemResponse instead of Item").
- Reference project rules (e.g. controller thin, no entities in API, no swallowed exceptions).
