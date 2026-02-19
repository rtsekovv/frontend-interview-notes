# Testing Interview Questions

## Types of Testing

<details>
<summary><b>What are the different types of testing (unit, integration, e2e)?</b></summary>

- **Unit tests**: Test single function/component in isolation. Fast, many of them. Mock dependencies
- **Integration tests**: Test how multiple units work together. Test API endpoints, database queries
- **E2E tests**: Test full user flows. Slow, expensive. Use Cypress, Playwright. Test critical paths only
</details>

<details>
<summary><b>How do you decide what to test?</b></summary>

Prioritize: critical business logic, edge cases, bug-prone areas, frequently changed code. Don't test: third-party libraries, trivial code, implementation details. Focus on behavior, not implementation. Follow test pyramid.
</details>

## Jest

<details>
<summary><b>What is Jest and how do you use it?</b></summary>

Jest is JavaScript testing framework by Meta. Features: zero config, snapshot testing, mocking, code coverage, watch mode. Use: `describe` for grouping, `it`/`test` for test cases, `expect` for assertions.
</details>

<details>
<summary><b>How do you write a basic unit test?</b></summary>

```javascript
describe('add function', () => {
  it('should add two numbers', () => {
    expect(add(2, 3)).toBe(5);
  });

  it('should handle negative numbers', () => {
    expect(add(-1, 1)).toBe(0);
  });
});
```
</details>

## Sinon

<details>
<summary><b>What is Sinon and when would you use it?</b></summary>

Sinon is library for test spies, stubs, and mocks. Use when: need to track function calls, replace dependencies, control time, fake servers. Often used with Jest or Mocha. Alternatives: Jest's built-in mocking.
</details>

## Stubs, Mocks & Spies

<details>
<summary><b>What is the difference between stubs, mocks, and spies?</b></summary>

- **Spy**: Wraps real function, records calls, lets original run. Use to verify calls
- **Stub**: Replaces function with controlled behavior. Use to control dependencies
- **Mock**: Stub with built-in expectations. Verifies correct calls were made
</details>

## Unit & Integration Tests

<details>
<summary><b>How do you add unit and integration tests to a project?</b></summary>

Setup: install Jest/Vitest, configure (jest.config.js), add test scripts to package.json. Create `__tests__` folders or `.test.js` files. Unit: test pure functions, components with Testing Library. Integration: test API routes, database operations with test database.
</details>

## TDD (Test-Driven Development)

<details>
<summary><b>What is TDD (Test-Driven Development)?</b></summary>

Write tests before code. Cycle: Red (write failing test) → Green (write minimal code to pass) → Refactor (improve code, keep tests passing). Benefits: better design, confidence, documentation. Not always practical, use where it helps.
</details>

<details>
<summary><b>Describe your experience with TDD</b></summary>

(Personal experience question - describe: projects where used, benefits observed, challenges, when you choose TDD vs test-after, how strict you follow it.)
</details>

## Test Pyramid

<details>
<summary><b>What is the Test Pyramid?</b></summary>

Testing strategy shape:
- **Top (few)**: E2E tests - slow, expensive, test critical paths
- **Middle (some)**: Integration tests - test component interactions
- **Bottom (many)**: Unit tests - fast, cheap, test logic in isolation

More tests at bottom, fewer at top.
</details>

<details>
<summary><b>How do you balance different types of tests in a project?</b></summary>

Follow pyramid: ~70% unit, ~20% integration, ~10% E2E. Adjust based on: app type (UI-heavy needs more E2E), team capacity, CI time limits. Focus unit tests on logic, E2E on critical user journeys.
</details>

## Test Coverage

<details>
<summary><b>How do you ensure adequate test coverage?</b></summary>

Use coverage tools (Jest --coverage). Aim for 70-80%, not 100%. Focus on: critical paths, complex logic, edge cases. Don't chase metrics - meaningful tests matter more than percentage. Review untested code manually.
</details>

## Testing Trophy

<details>
<summary><b>What is the Testing Trophy and how does it differ from the Test Pyramid?</b></summary>

**Testing Trophy** (Kent C. Dodds) is an alternative to Test Pyramid, more suited for frontend:

```
      E2E (few)
   Integration (most)
    Unit (some)
  Static (linting, types)
```

**Key difference:** More integration tests, fewer unit tests.

**Rationale:**
- Unit tests on implementation details break easily
- Integration tests on behavior are more valuable
- Frontend logic is often in UI interactions

**Proportions:**
- Static analysis (TypeScript, ESLint): Catches many bugs for free
- Unit tests: Pure functions, utilities, reducers
- Integration tests: Components with user interactions (React Testing Library)
- E2E tests: Critical user journeys only

**When to use which:**
- **Pyramid**: Backend, complex business logic, pure functions
- **Trophy**: Frontend-heavy apps, UI components, behavior testing

**Interview answer:** "I follow the pyramid as a cost principle, but for frontend I often shift toward integration tests that test behavior, keeping unit tests for pure logic - similar to the testing trophy approach."
</details>
