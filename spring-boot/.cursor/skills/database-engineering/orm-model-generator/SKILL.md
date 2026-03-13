---
name: orm-model-generator
description: Generates JPA entities and Spring Data repositories from schema or requirements. Use when creating or updating entity classes and repository interfaces for Java/Spring.
---

# ORM Model Generator

## When to Apply

Use when the user needs JPA entity classes or Spring Data repository interfaces (e.g. for a new table or schema change).

## Conventions (Java / Spring Data JPA)

- **Entities**: JPA `@Entity`, `@Table`, `@Id` (and `@GeneratedValue` if applicable). Use `@Column`, `@Enumerated`, `@Temporal`, and relationships (`@OneToOne`, `@OneToMany`, `@ManyToOne`, `@ManyToMany`) with appropriate fetch and cascade. Prefer wrapper types (e.g. `Long`) for nullable ids.
- **Repositories**: Interface extending `JpaRepository<Entity, Id>`. Prefer derived query methods; use `@Query` (JPQL) when naming is unclear or logic is complex. Return `Optional<T>` for single result, `List`/`Page`/`Slice` with `Pageable` for lists.
- **Naming**: Entity class singular (e.g. `Item`); table name plural or as per schema. Repository: `ItemRepository`, methods `findBy...`, `existsBy...`, `countBy...`, `deleteBy...`.
- **Project alignment**: Place entities in `model`/`entity` package, repositories in `repository` package. No business logic in entities; keep repositories as data access only.

## Output

- Entity class(es) with fields, annotations, and relationships.
- Repository interface(es) with method signatures (and `@Query` if needed).
- Brief note on lazy vs eager and cascade if non-default.
