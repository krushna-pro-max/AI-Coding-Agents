---
name: mock-service-builder
description: Builds mock implementations and test doubles for services, repositories, and external APIs in Java/Spring Boot tests. Use when creating mocks, stubs, or test doubles for unit or integration tests.
---

# Mock Service Builder

## When to Apply

Use when the user needs mock implementations of services, repositories, or external clients (e.g. REST, messaging) for tests. Covers both Mockito mocks and hand-written test doubles (stubs/fakes).

## Conventions

- **Mockito**: Prefer `@Mock` + `when(...).thenReturn(...)` for unit tests. Use `ArgumentCaptor` when you need to assert on arguments; use `verify` sparingly (focus on outcomes).
- **Stubs**: When a simple in-memory implementation is clearer (e.g. `FakeFooRepository` implementing `FooRepository`), implement the interface and keep state in memory. Use in integration tests or when behavior is complex to express with Mockito.
- **External APIs**: For REST clients, use MockWebServer (OkHttp) or WireMock, or mock the client bean with `@MockBean` and stub responses. Never call real external APIs in tests.
- **Spring**: Use `@MockBean` in `@SpringBootTest` or `@WebMvcTest` to replace a real bean with a mock. Use `@TestConfiguration` + `@Primary` to provide a test double bean when needed.
- **Consistency**: Document stub behavior (e.g. "returns empty list by default") and keep stub state predictable; reset or create fresh instance per test if stateful.

## Output

- Mock setup code (Mockito `when`/`thenReturn`/`thenThrow`) for the scenario, or
- A small test double class (e.g. `FakePaymentClient`) implementing the interface with minimal in-memory behavior, plus how to register it (e.g. `@TestConfiguration`).
- Brief note on when to use mock vs stub (mock for unit tests with injected dependency; stub when multiple tests share the same fake behavior or integration tests need a controllable implementation).

## Example Snippets

**Mockito mock in unit test:**
```java
when(paymentClient.charge(any(BigDecimal.class))).thenReturn(ChargeResult.success("tx-1"));
when(paymentClient.charge(eq(BigDecimal.ZERO))).thenThrow(new InvalidAmountException());
```

**Stub implementation for tests:**
```java
public class InMemoryOrderRepository implements OrderRepository {
    private final Map<Long, Order> store = new ConcurrentHashMap<>();
    private final AtomicLong idGen = new AtomicLong(1);

    @Override
    public Order save(Order order) {
        var id = order.getId() == null ? idGen.getAndIncrement() : order.getId();
        var saved = new Order(id, order.getItems());
        store.put(id, saved);
        return saved;
    }

    @Override
    public Optional<Order> findById(Long id) {
        return Optional.ofNullable(store.get(id));
    }
}
```

**Registering stub in test slice:**
```java
@TestConfiguration
static class Config {
    @Bean
    @Primary
    OrderRepository orderRepository() {
        return new InMemoryOrderRepository();
    }
}
```

## Guidelines

- Do not over-mock: avoid mocking the class under test or mocking value objects. Mock only external or heavy dependencies.
- Prefer meaningful return values over generic `null`/empty unless testing null/empty handling.
- For async code, use `CompletableFuture.completedFuture(...)` or Mockito `thenReturn(CompletableFuture.completedFuture(...))` so tests stay deterministic.
