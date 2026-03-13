---
name: edge-case-test-creator
description: Designs and generates tests for edge cases: null/empty inputs, boundaries, validation failures, and error paths in Java/Spring Boot. Use when strengthening test suites, testing validation, or when the user asks for edge-case or boundary tests.
---

# Edge Case Test Creator

## When to Apply

Use when the user wants to add tests for edge cases, boundary conditions, validation, or error paths. Complements unit and integration tests by focusing on "what if" scenarios.

## Conventions

- **Categories**:
  - **Null/empty**: `null` arguments, empty `String`, empty `List`/`Collection`, empty `Optional`. Expect validation exception or defined behavior (e.g. empty result), not NPE.
  - **Boundaries**: Min/max values (e.g. `Integer.MAX_VALUE`), zero, negative numbers where invalid, length limits (e.g. string length at limit and one over).
  - **Validation**: Invalid format (email, date), wrong type or range. Assert 400 or domain exception and message/code when relevant.
  - **Error paths**: Repository not found → 404 or `ResourceNotFoundException`; external service failure → retry or mapped exception; concurrent update → conflict or clear behavior.
- **Naming**: `methodName_edgeCaseDescription_expectedBehavior` or clear `@DisplayName`, e.g. "returns 400 when name is blank".
- **Assertions**: Assert both the outcome (status, exception type) and, when useful, the message or error body (e.g. validation field path). Use `assertThrows` and, if needed, `assertThat(exception.getMessage()).contains(...)`.
- **No silent passes**: Avoid tests that "pass" by not throwing; assert the positive behavior (e.g. empty list returned, specific exception).

## Output

- New test methods in an existing test class or a dedicated edge-case test class (e.g. `OrderServiceEdgeCaseTest`).
- One or more scenarios per edge category as relevant: null/empty, boundary, validation, error path.
- Clear arrange (e.g. invalid input), act (call method or HTTP request), assert (status/exception/body).
- Optional: a short table or list of "edge cases covered" for documentation.

## Example Scenarios

| Scenario | Input / Condition | Expected |
|----------|-------------------|----------|
| Null ID | `findById(null)` | `IllegalArgumentException` or 400 |
| Empty name | `CreateItemRequest("")` or `"   "` | 400, validation error on `name` |
| List empty | `processItems(Collections.emptyList())` | Empty result or no-op, no exception |
| Not found | `findById(999L)` where 999 does not exist | `ResourceNotFoundException` or 404 |
| Boundary | `quantity = 0` or `quantity = -1` | Validation failure or 400 |
| Overflow risk | Very large number where applicable | Defined behavior or validation |

## Example Snippet

```java
@ParameterizedTest
@NullAndEmptySource
@DisplayName("create rejects blank name")
void create_whenNameBlank_returns400(String name) {
    var request = new CreateItemRequest(name);
    mockMvc.perform(post("/api/v1/items")
            .contentType(APPLICATION_JSON)
            .content(toJson(request)))
        .andExpect(status().isBadRequest())
        .andExpect(jsonPath("$.errors").isArray());
}

@Test
@DisplayName("findById throws when not found")
void findById_whenMissing_throwsResourceNotFound() {
    when(service.findById(999L)).thenThrow(new ResourceNotFoundException("Order", 999L));
    assertThrows(ResourceNotFoundException.class, () -> controller.getById(999L));
}
```

## Guidelines

- Align with project validation: if Bean Validation is used, edge-case tests should trigger constraint violations and assert on the API error shape (e.g. `@Valid` + controller advice).
- Prefer parameterized tests (`@ParameterizedTest` with `@NullSource`, `@EmptySource`, `@ValueSource`, `@CsvSource`) for multiple equivalent edge inputs to keep tests DRY.
- Document the chosen behavior for "ambiguous" edges (e.g. "we treat null list as empty list") in a comment or `@DisplayName` so future changes are intentional.
