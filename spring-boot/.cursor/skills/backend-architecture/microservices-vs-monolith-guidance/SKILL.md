---
name: microservices-vs-monolith-guidance
description: Guides choice between monolith, modular monolith, and microservices based on team, domain, and ops. Use when deciding architecture style or planning a migration path.
---

# Microservices vs Monolith Guidance

## When to Apply

Use when the user is choosing architecture style (monolith vs microservices) or planning a migration.

## Context First

Consider: team size, deployment cadence, domain boundaries, operational maturity, failure isolation needs.

## Recommendations

- **Monolith-friendly**: Single team, unclear boundaries, need for simplicity and fast iteration, limited ops maturity → recommend modular monolith or well-structured monolith first.
- **Microservices-friendly**: Clear bounded contexts, multiple teams owning different domains, need for independent scaling/deployment, readiness for distributed systems complexity → discuss decomposition and integration patterns.

## Output

- Short decision frame (questions + criteria).
- A recommendation (monolith / modular monolith / microservices) with rationale.
- Migration path if moving from monolith to services (e.g. strangler fig, extract domain first).
