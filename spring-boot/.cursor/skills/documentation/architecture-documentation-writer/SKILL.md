---
name: architecture-documentation-writer
description: Writes architecture documentation: components, layers, data flow, and decisions. Use when documenting system design or ADRs.
---

# Architecture Documentation Writer

## When to Apply

Use when the user needs architecture docs: high-level design, components, layers, data flow, or decision records (e.g. for a Java/Spring Boot app).

## Content

- **Overview**: What the system does and main architectural style (e.g. layered, hexagonal, modular monolith).
- **Components / layers**: Controllers, services, repositories, external integrations; responsibility of each and how they interact.
- **Data flow**: Request path (e.g. API → controller → service → repository → DB) and key boundaries (e.g. DTOs at API edge).
- **Key decisions**: Technology choices, patterns (e.g. JWT auth, centralized error handling), and rationale. Optionally use ADR format (context, decision, consequences).
- **Diagrams**: Prefer Mermaid (flowchart, C4-style, or sequence) when it clarifies; keep in the same doc or link.

## Output

- Markdown doc (e.g. `docs/architecture.md` or `docs/README.md`) with clear headings. Use lists and optional Mermaid blocks. Reference existing docs (e.g. API docs, README) where relevant.
