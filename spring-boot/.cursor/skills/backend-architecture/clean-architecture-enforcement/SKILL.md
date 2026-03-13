---
name: clean-architecture-enforcement
description: Enforces Clean Architecture layers, dependency rule, and ports/adapters. Use when reviewing or generating code for layer violations, dependency direction, or hexagonal/onion structure.
---

# Clean Architecture Enforcement

## When to Apply

Use when reviewing or generating backend code for correct layering and dependency direction.

## Rules

- **Layers**: Clear separation—**domain** (entities, domain logic), **application/use cases** (orchestration, ports), **infrastructure** (adapters: DB, HTTP, messaging), **interfaces** (API, CLI).
- **Dependency rule**: Dependencies point **inward**. Domain has no dependencies on outer layers; infrastructure and interfaces depend on application/domain.
- **Ports and adapters**: Define ports (interfaces) in the application layer; implement adapters in infrastructure. Keep framework and I/O at the edges.

## When Reviewing or Generating Code

- Flag violations (e.g. domain importing from infrastructure).
- Suggest moving logic to the correct layer.
- Recommend interfaces (ports) where concrete implementations are used.
