---
name: bug-fix-suggestions
description: Suggests concrete code or config changes to fix bugs identified from stack traces or root cause. Use when the user wants fix options after analysis.
---

# Bug Fix Suggestions

## When to Apply

Use when a bug or failure has been analyzed (stack trace, root cause, or logs) and the user needs **concrete fix options** (code or config).

## Process

1. **Anchor to root cause**: Tie the fix to the identified root cause (e.g. NPE → null check or `Optional`, constraint violation → validation or schema).
2. **Minimal change**: Prefer the smallest change that fixes the issue (e.g. fix one method, add one validation) without unnecessary refactors unless requested.
3. **Alternatives**: If multiple valid fixes exist (e.g. fix at controller vs service, or validate vs allow null), list options with pros/cons.
4. **Verification**: Suggest how to confirm the fix (unit test, integration test, or manual step). Mention regression risk if relevant.

## Output

- One primary fix: code snippet or config change with brief explanation.
- Optional: alternative approaches and when to use them.
- How to verify (test or repro scenario).
- Align with project conventions (e.g. validation in service, errors via `@ControllerAdvice`, no swallowed exceptions).
