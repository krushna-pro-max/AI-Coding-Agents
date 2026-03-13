---
name: code-comment-generator
description: Generates or improves code comments: Javadoc, class/method summaries, and inline clarification. Use when adding or refining documentation in code.
---

# Code Comment Generator

## When to Apply

Use when the user wants to add or improve comments in code (Java/Spring Boot): Javadoc, class-level summary, or targeted inline comments.

## Conventions

- **Javadoc**: Use for public APIs (controllers, services, key public methods): `@param`, `@return`, `@throws` where they add value. One-line summary first; longer description only when behavior is non-obvious.
- **Class-level**: Brief purpose of the class (e.g. "REST controller for item resource", "JWT validation filter"). Avoid restating the type name.
- **Inline**: Comment only when intent or constraint is not clear from the code (e.g. business rule, workaround). Prefer clear naming over comments; use `_` for unused params (Java 21) instead of commenting them out.
- **Don’t**: Redundant comments that repeat the code; outdated comments. Keep comments in sync with code changes.

## Output

- Javadoc blocks for specified classes or methods (copy-paste ready).
- Short guideline when to add vs skip comments (e.g. self-explanatory getters need no Javadoc).
