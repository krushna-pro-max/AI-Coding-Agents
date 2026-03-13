---
name: deployment-script-generator
description: Generates deployment and ops scripts (start/stop, health checks, rollback). Use when automating deploy steps, releases, or operational runbooks.
---

# Deployment Script Generator

## When to Apply

Use when the user needs shell (or other) scripts for deploying an app, running health checks, performing rollbacks, or other repeatable ops tasks.

## Conventions

- **Idempotency**: Where possible, scripts should be safe to run multiple times (e.g. create dir if not exists, update in place). Document any non-idempotent steps clearly.
- **Exit codes**: Use standard exit codes: 0 for success, non-zero for failure. Exit immediately on critical errors unless the script explicitly handles retries.
- **Logging**: Echo clear, timestamped messages for major steps and errors; avoid logging secrets. Prefer stderr for error/diagnostic output when appropriate.
- **Rollback**: If the script performs a deploy, provide or document a rollback path (e.g. previous artifact, revert command, or link to runbook).
- **Environment**: Scripts should rely on env vars or config files for environment-specific values (URLs, paths, credentials). Do not hardcode secrets; document required env in a header or README.
- **Portability**: Prefer POSIX-compliant shell where possible; if using Bash-specific features, set shebang `#!/usr/bin/env bash` and note the requirement.

## Common Script Types

- **Start/stop**: Start app (e.g. JAR with `java` or via systemd/docker); stop gracefully (SIGTERM, then timeout and SIGKILL). Check process or health endpoint after start.
- **Health check**: Curl or wget to health endpoint; exit 0 only when HTTP 200 (or defined success criteria).
- **Deploy**: Pull artifact, backup current, switch symlink or copy, restart service, run health check; on failure, optionally restore backup and restart (rollback).
- **Backup/restore**: Document or script backup of DB or critical state; restore steps with clear ordering and checks.

## Output

- Script file(s) with shebang and brief header comment (purpose, usage, required env).
- List of required environment variables or config paths.
- Optional one-line runbook steps (when to run, how to rollback).
