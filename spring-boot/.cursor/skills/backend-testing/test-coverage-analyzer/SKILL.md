---
name: test-coverage-analyzer
description: Analyzes test coverage reports (JaCoCo, IDE) and recommends where to add or improve tests. Use when reviewing coverage, identifying untested code, or when the user asks for coverage analysis or improvement.
---

# Test Coverage Analyzer

## When to Apply

Use when the user has coverage data (e.g. JaCoCo report, IDE coverage run) or wants to know where tests are missing or weak. Focus on actionable recommendations, not only on percentage targets.

## Conventions

- **Tool**: Assume JaCoCo for Java (XML or HTML report). Key metrics: line coverage, branch coverage. Understand that 100% line coverage does not imply full branch or path coverage.
- **Priorities**: Critical paths (auth, payments, core business logic) and public API (controllers, service entry points) first. Then repositories and shared utilities. Avoid recommending tests for trivial getters/setters or generated code unless they carry logic.
- **Context**: Prefer "this method has no tests and handles validation" over "line 42 is uncovered." Tie recommendations to behavior and risk.
- **Format**: Summarize current state (e.g. "Controller X has ~60% line coverage"), list gaps (uncovered branches, missing exception paths), then suggest concrete test cases or test classes to add.
- **Exclusions**: Respect project exclusions (e.g. DTOs, config, main method). Do not suggest covering excluded code unless the user asks.

## Output

- Short summary of coverage (if user provided report or paths): what is well covered vs. under-covered.
- List of gaps: specific classes/methods or branches that are untested or only partially tested, with risk or behavior noted.
- Prioritized recommendations: 1–3 high-value test additions (e.g. "Add integration test for POST /orders"), then optional further items.
- If no report is available: suggest how to run coverage (e.g. `mvn test jacoco:report`) and where to find the report, then re-analyze once available.

## Example Summary Format

```markdown
## Coverage summary
- **OrderService**: ~85% line, ~70% branch. Missing: branch when `stock < quantity`, exception when payment fails.
- **OrderController**: ~60% line. Missing: 400 on invalid body, 404 when order not found.

## Recommendations
1. **High**: Add `OrderServiceTest` case: `placeOrder_whenInsufficientStock_throwsInsufficientStockException`.
2. **High**: Add `OrderControllerIntegrationTest`: `createOrder_withInvalidPayload_returns400`.
3. **Medium**: Add branch test for `OrderService.cancel` when order already shipped.
```

## JaCoCo Usage

- Report path often: `target/site/jacoco/jacoco.xml` or `build/reports/jacoco/test/html/`.
- To generate: `mvn clean test jacoco:report` (with JaCoCo plugin). Spring Boot projects often have it; if not, add the plugin and optionally set exclusions (e.g. `*Application.class`, `**/dto/**`).
