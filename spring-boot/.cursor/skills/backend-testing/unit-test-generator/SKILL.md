---
name: unit-test-generator
description: Generates JUnit 5 unit tests for Java/Spring Boot classes (services, utilities, mappers). Use when writing or adding unit tests, testing business logic in isolation, or when the user asks for unit tests.
---

# Unit Test Generator

## When to Apply

Use when the user needs unit tests for services, utilities, mappers, or other classes where dependencies can be mocked. Target: Java 21, JUnit 5, Mockito.

## Conventions

- **Framework**: JUnit 5 (`@Test`), Mockito for mocks. Use `@ExtendWith(MockitoExtension.class)` or `@Mock`/`@InjectMocks` for constructor-injected classes.
- **Naming**: `methodName_scenario_expectedOutcome` or `whenX_thenY`. One logical behavior per test.
- **Isolation**: Mock all collaborators; no real DB, HTTP, or file I/O. Tests must be fast and deterministic.
- **Assertions**: Prefer AssertJ (`assertThat(...).isEqualTo(...)`) or JUnit 5 `assertAll` for multiple checks. Use `assertThrows` for exception paths.
- **Structure**: Arrange–Act–Assert; avoid logic in tests. Use `@DisplayName` for readability.

## Output

- A test class in the same package under `src/test/java` (e.g. `FooService` → `FooServiceTest`).
- Test methods for happy path, main error paths, and key edge cases (null/empty, validation).
- Mock setup with `when(...).thenReturn(...)` or `thenThrow`; verify interactions only when they matter (e.g. "repository was called once").

## Example Snippet

```java
@ExtendWith(MockitoExtension.class)
@DisplayName("FooService")
class FooServiceTest {

    @Mock
    private FooRepository fooRepository;

    @InjectMocks
    private FooService fooService;

    @Test
    @DisplayName("findById returns entity when present")
    void findById_whenExists_returnsEntity() {
        var id = 1L;
        var entity = new Foo(id, "name");
        when(fooRepository.findById(id)).thenReturn(Optional.of(entity));

        var result = fooService.findById(id);

        assertThat(result).isPresent().get().isEqualTo(entity);
    }

    @Test
    @DisplayName("findById throws when not found")
    void findById_whenMissing_throws() {
        when(fooRepository.findById(1L)).thenReturn(Optional.empty());
        assertThrows(ResourceNotFoundException.class, () -> fooService.findById(1L));
    }
}
```

## Dependencies

Ensure `spring-boot-starter-test` (includes JUnit 5, Mockito, AssertJ) is present. Exclude JUnit 4 if present to avoid confusion.
