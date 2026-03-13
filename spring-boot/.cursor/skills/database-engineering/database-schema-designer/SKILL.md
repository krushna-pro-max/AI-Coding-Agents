---
name: database-schema-designer
description: Designs normalized database schemas, tables, relationships, and constraints. Use when defining or evolving data models, ER design, or reviewing schema for integrity and consistency.
---

# Database Schema Designer

## When to Apply

Use when the user needs to design or refine a database schema: new tables, relationships, constraints, or normalization.

## Process

1. **Gather requirements**: Identify entities, attributes, and relationships from the domain or user story.
2. **Normalize**: Apply normal forms (at least 3NF) where appropriate; denormalize only with justified trade-offs (e.g. read performance).
3. **Define structures**: Tables, primary keys, foreign keys, unique constraints, check constraints, and NOT NULL where required.
4. **Document**: Provide DDL or a clear schema description (column names, types, constraints). Optionally include a simple ER or Mermaid diagram.

## Output

- Table definitions with columns, types, and constraints.
- Relationship and cardinality (one-to-one, one-to-many, many-to-many with junction table).
- Rationale for key and constraint choices; note any assumptions (e.g. target DB: PostgreSQL, MySQL).
