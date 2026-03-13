---
name: naming-convention-validator
description: Validates naming conventions for packages, classes, methods, and variables in Java/Spring projects. Use when checking or enforcing naming standards.
---

# Naming Convention Validator

## When to Apply

Use when the user wants to check or enforce naming conventions (Java/Spring Boot, project rules).

## Conventions (align with project rules)

- **Packages**: Lowercase, reverse domain; group by feature or layer (e.g. `controller`, `service`, `repository`, `model`, `dto`, `config`, `exception`).
- **Classes**: PascalCase. Suffixes: `*Controller`, `*Service`, `*Repository`; DTOs: `*Request`, `*Response`, `*Dto`; entities: singular noun (e.g. `Item`, `User`).
- **Methods/variables**: camelCase. REST handlers: verb or `get*`, `create*`, `update*`, `delete*`. Meaningful names; avoid single letters except loop index or lambda (e.g. `e` for exception). Use `_` for intentionally unused (Java 21).
- **Constants**: UPPER_SNAKE_CASE when static final.

## Process

1. **Scan**: Check package names, class names in the changed or specified files, method and variable names.
2. **Flag**: List any name that does not match (e.g. controller not ending in `Controller`, DTO not `*Request`/`*Response`, unclear or single-letter variable where it hurts readability).
3. **Suggest**: Propose a compliant or clearer name with brief reason.

## Output

- Table or list: current name, location, suggested name, rule (e.g. "Controllers: *Controller").
- Focus on public API and types (controllers, services, DTOs) first; then notable locals if relevant.
