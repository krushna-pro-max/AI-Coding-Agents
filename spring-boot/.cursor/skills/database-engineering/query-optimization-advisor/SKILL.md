---
name: query-optimization-advisor
description: Advises on SQL and JPQL query optimization: execution plans, N+1, joins, and bottlenecks. Use when improving slow queries or reviewing query performance.
---

# Query Optimization Advisor

## When to Apply

Use when the user has slow queries, N+1 issues, or wants to improve SQL/JPQL performance (e.g. Spring Data JPA, raw SQL).

## Process

1. **Understand the query**: See the current SQL/JPQL, ORM usage (e.g. lazy loading, fetch joins), and access patterns.
2. **Identify issues**: N+1 selects, missing fetch joins, unnecessary columns, Cartesian products, inefficient predicates (e.g. functions on indexed columns), full table scans.
3. **Recommend changes**: Add fetch joins or entity graphs, restrict selected columns, add or adjust indexes (see Index Recommendation Engine skill), rewrite predicates to be index-friendly, use pagination (Page/Slice).
4. **Validate**: Suggest how to verify (EXPLAIN, query logs, profiling). Prefer JPQL over native when portability matters; use native when DB-specific features are needed.

## Output

- Concrete before/after query (or method) with brief explanation.
- List of changes and expected impact.
- How to confirm improvement (e.g. EXPLAIN ANALYZE, Hibernate stats).
