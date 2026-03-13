---
name: error-log-interpreter
description: Interprets error logs, log levels, and log context to pinpoint failures. Use when analyzing log output or configuring logging.
---

# Error Log Interpreter

## When to Apply

Use when the user shares log output (e.g. Spring Boot, Tomcat, or test logs) or asks how to interpret or improve logging for debugging.

## Process

1. **Level and message**: Identify ERROR/WARN/INFO and the main message; note timestamp and thread if present.
2. **Context**: Extract correlation IDs, request path, user or entity IDs, and any attached stack trace or exception block.
3. **Sequence**: If multiple log lines, order them chronologically and infer the flow (e.g. request received → validation failed → 400 returned).
4. **Gaps**: Flag missing context (e.g. no request ID, no exception cause) and suggest what to log (e.g. `log.warn("Validation failed for request {}", requestId, ex)`).

## Output

- Summary: what failed, when in the flow, and key context (IDs, path).
- Parsed sequence of relevant log entries.
- Suggestions to improve log quality (structured fields, exception logging with cause, avoid logging secrets).
