---
name: system-architecture-design
description: Designs high-level system architecture: bounded contexts, components, communication patterns, and trade-offs. Use when defining or evolving system design, discussing scale and NFRs, or producing architecture diagrams.
---

# System Architecture Design

## When to Apply

Use when the user needs system design, component boundaries, communication patterns, or architecture documentation (e.g. Java/Spring Boot or other stacks).

## Process

1. **Understand the problem**: Clarify scale, constraints, non-functional requirements (latency, throughput, consistency, availability).
2. **Propose high-level architecture**: Identify bounded contexts, main components, and how they communicate (sync/async, APIs, events).
3. **Document decisions**: Explain trade-offs (e.g. eventual consistency vs strong consistency, CAP implications where relevant).
4. **Output**: Clear textual or diagrammatic (e.g. C4, Mermaid) descriptions of the system, with rationale for key choices.

## Output Format

- Use headings, lists, and optional Mermaid diagrams.
- State rationale for major decisions and trade-offs.
