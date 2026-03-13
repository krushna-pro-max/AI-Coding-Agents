---
name: environment-variable-manager
description: Manages env var design, documentation, validation, and templates (.env.example). Use when defining config for apps, containers, or pipelines; never stores real secrets in repo.
---

# Environment Variable Manager

## When to Apply

Use when the user needs to define, document, validate, or template environment variables for an application, Docker/Compose, or CI/CD.

## Conventions

- **Documentation**: Maintain a single source of truth (e.g. `.env.example` or `env.schema`) listing all variables with short descriptions and whether they are required or optional. No real secrets in repo.
- **Naming**: Use clear, consistent names (e.g. `DATABASE_URL`, `LOG_LEVEL`, `API_BASE_URL`). Prefer uppercase with underscores for env vars.
- **Validation**: Where possible, validate required vars at startup (e.g. Spring Boot `@ConfigurationProperties` with validation, or a small bootstrap check). Fail fast with a clear message if critical vars are missing.
- **Defaults**: Provide safe defaults only for non-sensitive, optional settings (e.g. `LOG_LEVEL=INFO`, `SERVER_PORT=8080`). Never default secrets (DB passwords, API keys) in code or example files.
- **Scopes**: Distinguish app runtime, build-time, and CI-only vars; document which are needed in which environment (local, staging, prod, CI).

## Spring Boot

- Use `application.yml` / `application.properties` with placeholders (e.g. `${DATABASE_URL}`) and optional `spring.config.import=optional:env:`. Document env overrides in `.env.example`.
- For sensitive values, reference env vars only; support integration with secret managers (e.g. Kubernetes secrets, AWS Secrets Manager) via env or config.

## Output

- `.env.example` (or equivalent) with variable names, comments, and example non-secret values.
- Optional: validation snippet or config class that checks required vars at startup.
- Short note on where to set vars (local file, CI, container runtime, secret manager).
