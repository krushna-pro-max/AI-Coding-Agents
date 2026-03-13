---
name: stack-trace-analyzer
description: Parses and explains Java stack traces: frames, causes, and where to look. Use when the user shares a stack trace or exception output.
---

# Stack Trace Analyzer

## When to Apply

Use when the user provides a stack trace (e.g. from IDE, logs, or test failure) and needs to understand what failed and where.

## Process

1. **Identify exception type**: Note the top-level exception class and message (e.g. `NullPointerException`, `IllegalArgumentException`, `DataIntegrityViolationException`).
2. **Walk the stack**: From top (first frame) downward, identify the first frame in **user/application code** (not JDK, Spring, or library internals). That is usually the call site where the failure manifested or was triggered.
3. **Chained causes**: If there is a `Caused by:`, repeat for each cause; the root cause is often at the bottom. Summarize the chain (e.g. "DB constraint violation → JPA flush → service save").
4. **Context**: Note thread name, and any repeated frames (e.g. recursion, loop) that might indicate a pattern.

## Output

- Exception type and message.
- First relevant application frame (class, method, line if present).
- Short cause chain summary.
- One-sentence "where to look" (file/method) and what to check (null, argument, DB, config).
