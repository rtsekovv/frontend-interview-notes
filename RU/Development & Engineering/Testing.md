# Вопросы для собеседования по Testing

## Типы тестирования

<details>
<summary><b>Какие бывают типы тестирования (unit, integration, e2e)?</b></summary>

- **Unit-тесты**: Тестируют отдельную функцию/компонент в изоляции. Быстрые, много таких. Mock зависимости
- **Integration-тесты**: Тестируют как несколько units работают вместе. Тестируют API endpoints, database queries
- **E2E-тесты**: Тестируют полные пользовательские сценарии. Медленные, дорогие. Используют Cypress, Playwright. Тестируйте только критические пути
</details>

<details>
<summary><b>Как вы решаете что тестировать?</b></summary>

Приоритизируйте: критическую бизнес-логику, edge cases, bug-prone области, часто изменяемый код. Не тестируйте: сторонние библиотеки, тривиальный код, детали реализации. Фокусируйтесь на поведении, не реализации. Следуйте test pyramid.
</details>

## Jest

<details>
<summary><b>Что такое Jest и как его использовать?</b></summary>

Jest — JavaScript testing framework от Meta. Фичи: zero config, snapshot testing, mocking, code coverage, watch mode. Используйте: `describe` для группировки, `it`/`test` для test cases, `expect` для assertions.
</details>

<details>
<summary><b>Как написать базовый unit-тест?</b></summary>

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
<summary><b>Что такое Sinon и когда его использовать?</b></summary>

Sinon — библиотека для test spies, stubs и mocks. Используйте когда: нужно отслеживать вызовы функций, заменять зависимости, контролировать время, fake servers. Часто используется с Jest или Mocha. Альтернативы: встроенный mocking в Jest.
</details>

## Stubs, Mocks и Spies

<details>
<summary><b>В чём разница между stubs, mocks и spies?</b></summary>

- **Spy**: Оборачивает реальную функцию, записывает вызовы, позволяет оригиналу выполниться. Используйте для проверки вызовов
- **Stub**: Заменяет функцию контролируемым поведением. Используйте для контроля зависимостей
- **Mock**: Stub со встроенными expectations. Проверяет что были сделаны правильные вызовы
</details>

## Unit и Integration Tests

<details>
<summary><b>Как добавить unit и integration тесты в проект?</b></summary>

Настройка: установите Jest/Vitest, настройте (jest.config.js), добавьте test scripts в package.json. Создайте папки `__tests__` или файлы `.test.js`. Unit: тестируйте pure functions, компоненты с Testing Library. Integration: тестируйте API routes, database operations с test database.
</details>

## TDD (Test-Driven Development)

<details>
<summary><b>Что такое TDD (Test-Driven Development)?</b></summary>

Пишите тесты до кода. Цикл: Red (напишите falling test) → Green (напишите минимальный код для прохождения) → Refactor (улучшите код, сохраняя тесты проходящими). Преимущества: лучший дизайн, уверенность, документация. Не всегда практичен, используйте где помогает.
</details>

<details>
<summary><b>Опишите ваш опыт с TDD</b></summary>

(Личный вопрос — опишите: проекты где использовали, наблюдаемые преимущества, сложности, когда выбираете TDD vs test-after, насколько строго следуете.)
</details>

## Test Pyramid

<details>
<summary><b>Что такое Test Pyramid?</b></summary>

Стратегия тестирования в форме пирамиды:
- **Верх (мало)**: E2E-тесты — медленные, дорогие, тестируют критические пути
- **Середина (несколько)**: Integration-тесты — тестируют взаимодействие компонентов
- **Низ (много)**: Unit-тесты — быстрые, дешёвые, тестируют логику в изоляции

Больше тестов внизу, меньше наверху.
</details>

<details>
<summary><b>Как вы балансируете разные типы тестов в проекте?</b></summary>

Следуйте пирамиде: ~70% unit, ~20% integration, ~10% E2E. Корректируйте исходя из: типа приложения (UI-heavy нуждается в большем количестве E2E), возможностей команды, лимитов времени CI. Фокусируйте unit-тесты на логике, E2E на критических пользовательских сценариях.
</details>

## Test Coverage

<details>
<summary><b>Как обеспечить достаточное покрытие тестами?</b></summary>

Используйте coverage tools (Jest --coverage). Стремитесь к 70-80%, не к 100%. Фокусируйтесь на: критических путях, сложной логике, edge cases. Не гонитесь за метриками — значимые тесты важнее процента. Ревьюите непокрытый код вручную.
</details>

## Testing Trophy

<details>
<summary><b>Что такое Testing Trophy и чем он отличается от Test Pyramid?</b></summary>

**Testing Trophy** (Kent C. Dodds) — альтернатива Test Pyramid, более подходящая для frontend:

```
      E2E (мало)
   Integration (больше всего)
    Unit (немного)
  Static (linting, types)
```

**Ключевое отличие:** Больше integration-тестов, меньше unit-тестов.

**Обоснование:**
- Unit-тесты на детали реализации легко ломаются
- Integration-тесты на поведение более ценны
- Frontend логика часто в UI взаимодействиях

**Пропорции:**
- Static analysis (TypeScript, ESLint): Ловит много багов бесплатно
- Unit-тесты: Pure functions, utilities, reducers
- Integration-тесты: Компоненты с пользовательскими взаимодействиями (React Testing Library)
- E2E-тесты: Только критические пользовательские сценарии

**Когда что использовать:**
- **Pyramid**: Backend, сложная бизнес-логика, pure functions
- **Trophy**: Frontend-heavy приложения, UI-компоненты, behavior testing

**Ответ для собеседования:** "Я следую пирамиде как принципу cost, но для frontend часто смещаюсь к integration-тестам, которые тестируют поведение, сохраняя unit-тесты для pure logic — похоже на подход testing trophy."
</details>
