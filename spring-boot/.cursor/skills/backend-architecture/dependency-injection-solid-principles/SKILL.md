---
name: dependency-injection-solid-principles
description: Applies Dependency Injection and SOLID (SRP, OCP, LSP, ISP, DIP) to backend code. Use when reviewing or generating code for DI and SOLID violations.
---

# Dependency Injection & SOLID Principles

## When to Apply

Use when reviewing or generating code for dependency injection style and SOLID adherence.

## Dependency Injection

- Prefer constructor injection; keep injection points explicit and minimal.
- Surfaces dependencies clearly and improves testability.

## SOLID

- **S**ingle Responsibility: One reason to change per class/module; split when a type does multiple jobs.
- **O**pen/Closed: Extend via new types or strategy/composition; avoid modifying stable code for new behavior where possible.
- **L**iskov Substitution: Subtypes must be usable where base types are expected without breaking contracts.
- **I**nterface Segregation: Small, focused interfaces; callers should not depend on methods they do not use.
- **D**ependency Inversion: Depend on abstractions (interfaces/ports); high-level logic should not depend on low-level details.

## When Reviewing or Generating Code

- Suggest interfaces for external or volatile dependencies.
- Point out SRP or DIP violations.
- Recommend constructor-injected services and small, cohesive interfaces.
