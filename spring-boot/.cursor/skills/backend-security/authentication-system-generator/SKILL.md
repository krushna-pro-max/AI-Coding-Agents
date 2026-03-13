---
name: authentication-system-generator
description: Generates authentication flows with JWT and Spring Security: login, filter chain, and user loading. Use when adding or refactoring authentication (JWT, form, or stateless).
---

# Authentication System Generator

## When to Apply

Use when the user needs to implement or refactor authentication (e.g. JWT-based) in Java/Spring Boot.

## Conventions (Spring Security + JWT)

- **Login**: Stateless login endpoint (e.g. POST `/api/v1/auth/login`) that validates credentials and returns a JWT (and optionally refresh token). Use a dedicated auth service; never return raw passwords.
- **Filter chain**: Configure `SecurityFilterChain`: permit public paths (login, health, docs), authenticate all other `/api/**` with JWT. Use `JwtAuthenticationFilter` (or equivalent) to validate token and set `SecurityContext`.
- **User loading**: Implement `UserDetailsService` (or custom `AuthenticationProvider`) that loads user by username/email from repository. Use constructor injection; keep passwords hashed (BCrypt).
- **Security config**: Prefer lambda DSL. Disable CSRF for stateless API; enable CORS explicitly if needed. Store secrets in config (e.g. `application.yml` / env), never in code.

## Output

- Auth controller (login endpoint), request/response records (e.g. `LoginRequest`, `TokenResponse`).
- Security config (`SecurityFilterChain`), JWT filter class, and `UserDetailsService` (or provider).
- Brief note on dependencies (e.g. `spring-boot-starter-security`, jjwt or Spring Security OAuth2 Resource Server for JWT).
