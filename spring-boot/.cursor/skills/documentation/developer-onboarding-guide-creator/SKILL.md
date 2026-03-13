---
name: developer-onboarding-guide-creator
description: Creates developer onboarding guides: env setup, first run, and where to find docs. Use when onboarding new developers to the project.
---

# Developer Onboarding Guide Creator

## When to Apply

Use when the user needs a guide for new developers: local setup, first run, and navigation (e.g. Java/Spring Boot repo).

## Content

- **Prerequisites**: Install list (JDK 21, Maven/Gradle, IDE, optional Docker/DB). Include version or link to project requirements.
- **Repository**: Clone, branch policy (e.g. main vs feature branches), and where key config lives (e.g. `application.yml`, env).
- **Setup**: Build and run (e.g. `./mvnw clean install`, `./mvnw spring-boot:run`). Required env vars or local config (no production secrets). DB: how to run locally (e.g. Docker, H2 for dev).
- **Verify**: How to confirm the app is up (e.g. health endpoint, Swagger UI URL). Run tests: `./mvnw test`.
- **Where to find more**: README, architecture doc, API docs (Swagger/OpenAPI), and code layout (packages, layers). Link to runbooks or ops docs if present.

## Output

- Single Markdown doc (e.g. `docs/onboarding.md` or section in README) with numbered or bullet steps. Use code blocks for commands. Keep it minimal so a new dev can run the app and tests in under 15 minutes with the stated prerequisites.
