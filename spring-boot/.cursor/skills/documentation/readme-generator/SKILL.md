---
name: readme-generator
description: Generates or improves project README files: overview, setup, run, and usage. Use when creating or updating README.md for a repository.
---

# README Generator

## When to Apply

Use when the user needs a new or updated README (e.g. project root `README.md`) for a Java/Spring Boot or other project.

## Structure

- **Title and brief description**: One-line project name and 1–3 sentence overview (what it does, for whom).
- **Prerequisites**: Runtime (e.g. Java 21, Maven/Gradle), optional DB or env (e.g. PostgreSQL, env vars).
- **Getting started**: Clone, build (e.g. `./mvnw clean install`), and run (e.g. `./mvnw spring-boot:run` or run main class). Include any required config (e.g. `application.yml` or env).
- **Configuration**: Key config options or env vars (no secrets); point to `application.yml` or docs if detailed.
- **Usage**: How to call the API (e.g. base URL, example curl or link to Swagger UI) or how to use the app.
- **Optional**: Testing (`./mvnw test`), project structure (short), license, contributing.

## Output

- Full or section-by-section README in Markdown. Use clear headings (`##`, `###`), code blocks for commands, and consistent formatting. Place in repo root unless the user specifies otherwise.
