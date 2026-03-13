---
name: migration-script-generator
description: Generates versioned database migration scripts (e.g. Flyway, Liquibase) for schema changes. Use when adding or altering tables, columns, or indexes in a repeatable way.
---

# Migration Script Generator

## When to Apply

Use when the user needs versioned migrations for schema changes (DDL) in a Java/Spring or other project using Flyway or Liquibase.

## Conventions

- **Versioning**: Use sequential version numbers or timestamps (e.g. `V1__create_items.sql`, `V2__add_user_id_to_items.sql`). Never edit an already-applied migration.
- **Idempotency / repeatability**: Prefer migrations that can be applied once safely (Flyway: run once per version). For Liquibase, use changeSet id + author for uniqueness.
- **Content**: One logical change per migration when practical. Include CREATE TABLE, ALTER TABLE, CREATE INDEX, and data backfills if needed. Use IF NOT EXISTS / IF EXISTS where the engine supports it to avoid failures on re-run (only when appropriate).
- **Rollback**: If the tool supports it (e.g. Liquibase rollback), provide rollback steps; otherwise document manual rollback or a compensating migration.

## Output

- Migration file(s) with correct naming and DDL (and optional DML).
- Short comment at top describing the change.
- Note on tool (Flyway vs Liquibase) and dialect if DB-specific (e.g. PostgreSQL).
