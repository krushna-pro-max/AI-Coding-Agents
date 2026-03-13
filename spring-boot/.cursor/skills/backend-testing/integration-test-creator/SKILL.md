---
name: integration-test-creator
description: Creates integration tests for REST APIs, repositories, and Spring components with real or contained dependencies. Use when adding or refactoring integration tests, testing endpoints end-to-end, or when the user mentions integration tests or Testcontainers.
---

# Integration Test Creator

## When to Apply

Use when the user needs integration tests that exercise controllers + service + repository (and optionally DB), or full HTTP request/response cycles. Target: Spring Boot Test, JUnit 5, optional Testcontainers.

## Conventions

- **Slice**: Prefer `@WebMvcTest` for controller-only (mocked services) or `@SpringBootTest` for full context. Use `@SpringBootTest(webEnvironment = WebEnvironment.RANDOM_PORT)` for real HTTP when needed.
- **HTTP**: Use `MockMvc` for `@WebMvcTest` or `TestRestTemplate` / `WebTestClient` for full server. Assert status, body, and headers.
- **Data**: Use `@Transactional` + repository save for in-memory H2, or Testcontainers for real DB. Clean state per test when possible (e.g. `@DirtiesContext` only if necessary).
- **Naming**: `method_httpMethod_scenario_expectedStatus` or descriptive `@DisplayName`. One meaningful scenario per test.
- **Configuration**: Use `@TestConfiguration` or `application-test.yml` for test-specific props (e.g. H2, disabled security if tested separately).

## Output

- Integration test class (e.g. `ItemControllerIntegrationTest`, `ItemRepositoryIntegrationTest`) under `src/test/java`.
- Test methods that perform real HTTP calls or real repository calls and assert outcomes.
- Clear setup (e.g. given data) and assertions on response status, body, or DB state.
- If Testcontainers is used: `@Testcontainers`, container definition, and `@DynamicPropertySource` for datasource URL.

## Example Snippets

**Controller with MockMvc:**
```java
@WebMvcTest(ItemController.class)
@Import(ItemService.class) // or mock if slicing
class ItemControllerIntegrationTest {

    @Autowired
    private MockMvc mockMvc;

    @MockBean
    private ItemService itemService;

    @Test
    void getById_whenExists_returns200AndBody() throws Exception {
        when(itemService.findById(1L)).thenReturn(new ItemResponse(1L, "item"));
        mockMvc.perform(get("/api/v1/items/1"))
            .andExpect(status().isOk())
            .andExpect(jsonPath("$.name").value("item"));
    }
}
```

**Full stack with Testcontainers:**
```java
@SpringBootTest(webEnvironment = WebEnvironment.RANDOM_PORT)
@Testcontainers
class ItemApiIntegrationTest {

    @Container
    static PostgreSQLContainer<?> postgres = new PostgreSQLContainer<>("postgres:15");

    @DynamicPropertySource
    static void props(DynamicPropertyRegistry registry) {
        registry.add("spring.datasource.url", postgres::getJdbcUrl);
        registry.add("spring.datasource.username", postgres::getUsername);
        registry.add("spring.datasource.password", postgres::getPassword);
    }

    @Autowired
    private TestRestTemplate restTemplate;

    @Test
    void createItem_returns201AndLocation() {
        var response = restTemplate.postForEntity("/api/v1/items",
            new CreateItemRequest("name"), ItemResponse.class);
        assertThat(response.getStatusCode()).isEqualTo(CREATED);
        assertThat(response.getBody()).isNotNull();
    }
}
```

## Dependencies

- `spring-boot-starter-test` for MockMvc, TestRestTemplate, test slices.
- Optional: `testcontainers` (and `postgresql` or `jdbc` module) for real DB integration tests.
