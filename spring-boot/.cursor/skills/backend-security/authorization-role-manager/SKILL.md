---
name: authorization-role-manager
description: Manages authorization with roles and Spring Security method security (@PreAuthorize, roles, permissions). Use when adding RBAC or protecting endpoints by role.
---

# Authorization Role Manager

## When to Apply

Use when the user needs role-based or permission-based access control (RBAC) on endpoints or methods.

## Conventions (Spring Security)

- **Roles**: Represent roles in the token (e.g. JWT claim `roles` or `authorities`) and as `GrantedAuthority`. Use a consistent prefix (e.g. `ROLE_ADMIN`, `ROLE_USER`) if using `hasRole()`.
- **Method security**: Enable with `@EnableMethodSecurity`. Use `@PreAuthorize("hasRole('ADMIN')")`, `@PreAuthorize("hasAuthority('READ_ITEMS')")`, or SpEL (e.g. `@PreAuthorize("@auth.canAccess(#id)")`) on service or controller methods.
- **URL-level**: Optionally restrict by path in `SecurityFilterChain` (e.g. `/api/v1/admin/**` requires `ROLE_ADMIN`). Prefer method security for fine-grained control.
- **Principle**: One source of truth for roles (e.g. from JWT or from DB after auth). Do not duplicate role logic in multiple layers.

## Output

- Example `@PreAuthorize` usage and optional `SecurityFilterChain` path matchers.
- How to expose roles in JWT (claims) and load `GrantedAuthority` in the authentication object.
- Optional custom SpEL method (e.g. `@auth.canAccess`) for resource-level checks.
