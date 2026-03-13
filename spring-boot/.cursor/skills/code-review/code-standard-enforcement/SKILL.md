---
name: code-standard-enforcement
description: Enforces project and Java/Spring Boot standards: layer rules, HTTP semantics, error handling, and conventions. Use when checking compliance with .cursor/rules and team standards.
---

# Code Standard Enforcement

## When to Apply

Use when the user wants to verify that code follows project standards (e.g. `.cursor/rules`, Java 21, Spring Boot conventions).

## Sources of Truth

- **Project rules**: Read `.cursor/rules/*.mdc` when present (java-spring-boot-standards, controller-layer, service-layer, repository-layer). Treat these as authoritative for the project.
- **Java 21**: Records for DTOs; pattern matching; `var` where type is obvious; `Optional.orElseThrow()`; sequenced collection access; no swallowed exceptions.
- **Spring Boot**: Constructor injection; `@RestController` + `@RequestMapping`; `ResponseEntity<T>`; versioned paths `/api/v1/...`; DTOs only at API boundary.
- **Layers**: Controllers thin (parse, validate, delegate, return); services hold business logic; repositories data access only; errors via `@ControllerAdvice`.

## Process

1. **Load rules**: If reviewing a layer (controller, service, repository), load the corresponding rule file.
2. **Check each convention**: Go through naming, structure, error handling, and layer boundaries.
3. **List violations**: For each violation, cite the rule and the file/line (or method). Suggest the compliant form.

## Output

- List of violations with rule reference (e.g. "Controller must not contain business logic — service-layer.mdc").
- Compliant example or one-line fix per violation.
- Optional: summary count by severity (must-fix vs should-fix).
