---
name: docker-configuration-generator
description: Generates Dockerfiles, docker-compose, and container config for apps (Java/Spring Boot, Node, etc.). Use when containerizing services, multi-stage builds, or defining compose stacks.
---

# Docker Configuration Generator

## When to Apply

Use when the user needs Dockerfiles, `.dockerignore`, docker-compose files, or container runtime config for an application or stack.

## Conventions

- **Multi-stage builds**: Use a build stage for compilation (Maven/Gradle/npm) and a minimal runtime stage (e.g. `eclipse-temurin:21-jre-alpine` for Java). Copy only artifacts and required files into the final image.
- **Non-root user**: Create and use a non-root user in the final stage; set correct ownership for app directories.
- **Base images**: Prefer official, minimal, and version-pinned images (e.g. `eclipse-temurin:21-jre-alpine`, `node:20-alpine`). Avoid `latest` in production Dockerfiles.
- **Layers**: Order Dockerfile instructions to maximize cache reuse (dependencies before app code). Use `.dockerignore` to exclude build artifacts, IDE files, and unnecessary content.
- **Health checks**: Add `HEALTHCHECK` (or equivalent in compose) for long-running services when the app exposes a health endpoint (e.g. Spring Boot actuator).
- **Secrets**: Never bake secrets into images. Use env vars, secrets files mounted at runtime, or a secret manager; document required env in comments or a separate env example.

## Java/Spring Boot

- Build: Use Maven or Gradle in builder stage; copy JAR (or native binary) to runtime stage.
- Runtime: `JAVA_OPTS` or `JVM_OPTS` via env for heap/tuning; port expose (e.g. 8080) documented.
- Optional: Use Spring Boot layered JAR and copy layers in Dockerfile for better layer caching.

## Output

- `Dockerfile` (and optional `.dockerignore`) for the app.
- Optional `docker-compose.yml` for local or single-host runs (app + DB/cache if needed).
- Short comment block at top of each file; list required env vars and ports.
