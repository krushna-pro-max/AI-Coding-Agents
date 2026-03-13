---
name: scalable-folder-structure-generator
description: Generates or proposes scalable folder/file structure for backends (e.g. by feature or layer). Use when defining or refactoring project layout.
---

# Scalable Folder Structure Generator

## When to Apply

Use when defining a new project structure or refactoring an existing layout (e.g. Java/Spring).

## Conventions

- Align with language and framework (e.g. Java/Spring: packages by feature or by layer; consistent naming).
- Structure should stay navigable as the codebase grows (e.g. feature-based or bounded-context-based folders, clear entry points per vertical).

## Output

- Propose or generate a **folder/file structure** (tree format or list) with brief rules (e.g. "controllers here", "domain entities here", "adapters here").
- Optionally generate stub files or README per area.
- Respect existing project layout when refactoring.
