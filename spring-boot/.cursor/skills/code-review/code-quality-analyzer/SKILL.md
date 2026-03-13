---
name: code-quality-analyzer
description: Analyzes code for readability, maintainability, complexity, and clarity. Use when reviewing code quality or assessing technical debt.
---

# Code Quality Analyzer

## When to Apply

Use when the user wants an assessment of code quality: readability, structure, complexity, or maintainability (e.g. Java/Spring Boot).

## Process

1. **Readability**: Check naming clarity, method length, nesting depth, and comment necessity (prefer self-documenting code; comment only when intent is non-obvious).
2. **Maintainability**: Single responsibility per class/method; low coupling; clear boundaries (controller vs service vs repository). Flag duplicated logic and suggest extraction.
3. **Complexity**: Note long methods, deep conditionals, or high cyclomatic complexity; suggest splitting or early returns.
4. **Consistency**: Align with project standards (Java 21, records for DTOs, constructor injection, layer responsibilities). Reference `.cursor/rules` when present.

## Output

- Summary: overall quality level and top 2–3 strengths/concerns.
- Bullet list of specific findings with file/method and brief suggestion.
- Prioritized: critical (e.g. logic errors, security) first, then maintainability, then style.
