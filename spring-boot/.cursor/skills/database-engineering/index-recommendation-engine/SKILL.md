---
name: index-recommendation-engine
description: Recommends database indexes for tables and queries: B-tree, composite, unique, partial. Use when adding indexes for performance or reviewing index strategy.
---

# Index Recommendation Engine

## When to Apply

Use when the user needs to add or review indexes for query performance, uniqueness, or foreign keys.

## Process

1. **Analyze access patterns**: Which columns are used in WHERE, JOIN, ORDER BY, GROUP BY? Which are used for uniqueness (e.g. natural keys)?
2. **Recommend index type**: B-tree for equality and range; composite index column order matters (equality columns first, then range). Consider unique indexes for natural keys.
3. **Avoid over-indexing**: Each index adds write cost. Prefer indexes that serve multiple queries; drop or defer indexes that are rarely used.
4. **Document**: Index name, table, columns, order, and whether unique. Note target DB if relevant (e.g. PostgreSQL, MySQL).

## Output

- DDL or migration snippet for creating (and optionally dropping) indexes.
- Short rationale: which query or constraint the index supports.
- Caveats (e.g. partial/conditional indexes) if applicable.
