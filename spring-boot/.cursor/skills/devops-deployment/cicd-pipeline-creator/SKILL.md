---
name: cicd-pipeline-creator
description: Creates CI/CD pipeline configs (GitHub Actions, GitLab CI, Jenkins, etc.) for build, test, and deploy. Use when setting up or updating pipelines, gates, or release automation.
---

# CI/CD Pipeline Creator

## When to Apply

Use when the user needs pipeline definitions for continuous integration and/or deployment (e.g. GitHub Actions, GitLab CI, Jenkinsfile, Azure Pipelines).

## Conventions

- **Deterministic builds**: Pin tool versions (Java, Node, Maven/Gradle) where possible. Use consistent caches (dependency cache, build cache) to speed runs and avoid flakiness.
- **Stages**: Separate build, test (unit + optional integration), lint/format, and deploy. Fail fast on build and tests before deploy.
- **Secrets**: Never log or echo secrets. Use the platform’s secret store (e.g. GitHub Secrets, GitLab CI variables masked). Reference secrets by name in the pipeline; document required secrets in a README or runbook.
- **Artifacts**: Build once and reuse the same artifact for test and deploy when possible. Use explicit versioning or commit SHA in artifact names/tags for traceability.
- **Deploy**: Prefer manual or approval gates for production; use env-specific jobs or workflows (e.g. staging auto, prod manual). Idempotent deploy steps.

## Common Platforms

- **GitHub Actions**: Use `actions/checkout`, version-pinned actions (e.g. `actions/setup-java` with `distribution` and `java-version`). Store dependency caches with `actions/cache` keyed by lockfile or manifest.
- **GitLab CI**: Define stages in `.gitlab-ci.yml`; use `rules` or `only` for branch/tag; cache `target/` or `node_modules/` as appropriate.
- **Jenkins**: Prefer declarative pipeline; use `environment {}` for env vars; run in agents with consistent tooling.

## Output

- Pipeline file(s) (e.g. `.github/workflows/ci.yml`, `.gitlab-ci.yml`, `Jenkinsfile`) with build, test, and optional deploy stages.
- Brief list of required secrets and any one-time setup (e.g. self-hosted runner, deploy keys).
