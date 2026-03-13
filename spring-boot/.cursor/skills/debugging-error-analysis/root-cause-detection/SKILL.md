---
name: root-cause-detection
description: Identifies the underlying root cause of failures from symptoms, logs, and code. Use when debugging recurring or non-obvious failures.
---

# Root Cause Detection

## When to Apply

Use when the user has a failure (test, runtime, or production) and needs to find the **underlying** cause, not just the immediate exception.

## Process

1. **Symptoms**: Gather what failed (status code, message, log line), when (after which change, which request), and reproducibility (always, sometimes, once).
2. **Hypotheses**: List plausible causes (e.g. null input, wrong config, race, DB state, wrong dependency version). Prioritize by likelihood and impact.
3. **Evidence**: Point to code paths, config, or logs that support or contradict each hypothesis. Suggest a minimal repro (unit test, curl, or script) to confirm.
4. **Root cause**: State the single most likely root cause and why; distinguish "trigger" (e.g. bad request) from "root cause" (e.g. missing validation, wrong assumption).

## Output

- Short summary of symptoms and reproducibility.
- Ranked hypotheses with evidence.
- Stated root cause and recommended fix or verification step.
- Optional: prevention (validation, tests, monitoring) to avoid recurrence.
