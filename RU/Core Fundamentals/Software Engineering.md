# Вопросы для собеседования по Software Engineering

## Debugging

<details>
<summary><b>Как вы отлаживаете код? Какие инструменты используете?</b></summary>

Использую browser DevTools (Chrome/Firefox) для frontend — breakpoints, console.log, вкладка network, performance profiler. Для Node.js — встроенный debugger или VS Code debugger. Также использую React DevTools, Redux DevTools для инспекции state. Начинаю с воспроизведения бага, затем пошагово сужаю область проблемы.
</details>

## Clean Code (SOLID, DRY, YAGNI, KISS)

<details>
<summary><b>Что такое SOLID? Объясните каждый принцип</b></summary>

- **S** - Single Responsibility: Класс должен иметь только одну причину для изменения
- **O** - Open/Closed: Открыт для расширения, закрыт для модификации
- **L** - Liskov Substitution: Дочерние классы должны быть заменяемы на родительские
- **I** - Interface Segregation: Много маленьких интерфейсов лучше, чем один большой
- **D** - Dependency Inversion: Зависеть от абстракций, а не от конкретных реализаций
</details>

<details>
<summary><b>Что такое DRY (Don't Repeat Yourself)?</b></summary>

Избегайте дублирования кода. Если пишете одну и ту же логику дважды, выносите её в функцию или модуль. Но не переусердствуйте с абстракциями — некоторое дублирование допустимо, если контексты различаются.
</details>

<details>
<summary><b>Что такое YAGNI (You Aren't Gonna Need It)?</b></summary>

Не реализуйте функциональность, пока она действительно не понадобится. Избегайте преждевременной оптимизации и создания функционала "на всякий случай". Фокусируйтесь на текущих требованиях.
</details>

<details>
<summary><b>Что такое KISS (Keep It Simple, Stupid)?</b></summary>

Пишите простой, читаемый код. Избегайте over-engineering. Простое решение, которое работает, лучше сложного "умного" решения. Вы в будущем (или коллеги) должны легко понять код.
</details>

## OOP

<details>
<summary><b>Объясните основы OOP (Object-Oriented Programming)</b></summary>

Четыре основных принципа:
- **Инкапсуляция**: Объединение данных и методов, сокрытие внутренних деталей
- **Абстракция**: Показ только необходимых деталей, сокрытие сложности
- **Наследование**: Дочерний класс наследует свойства/методы от родительского
- **Полиморфизм**: Один интерфейс, разные реализации (переопределение методов)
</details>

## MVC

<details>
<summary><b>Что такое MVC архитектура?</b></summary>

Паттерн Model-View-Controller разделяет приложение на три части:
- **Model**: Данные и бизнес-логика
- **View**: UI/слой представления (что видит пользователь)
- **Controller**: Обрабатывает пользовательский ввод, обновляет Model, выбирает View

Преимущества: разделение ответственности, упрощённое тестирование, параллельная разработка.
</details>

## CI/CD и статические анализаторы кода

<details>
<summary><b>Как вы настраиваете CI/CD?</b></summary>

Использую инструменты типа GitHub Actions, GitLab CI, Jenkins. Настройка включает: автоматические тесты на каждый PR, проверки линтером, процесс сборки, деплой на staging/production. Пример flow: push кода → запуск тестов → сборка → деплой на staging → ручное подтверждение → деплой на production.
</details>

<details>
<summary><b>Какие статические анализаторы кода вы используете?</b></summary>

ESLint для JavaScript/TypeScript (ловит ошибки, обеспечивает единый стиль), Prettier для форматирования, SonarQube для глубокого анализа (безопасность, code smells). Компилятор TypeScript тоже является статическим анализатором.
</details>

## Production Support и мониторинг

<details>
<summary><b>Как вы обеспечиваете production support и мониторинг?</b></summary>

Использую инструменты мониторинга: Sentry для отслеживания ошибок, DataDog/New Relic для мониторинга производительности, CloudWatch для AWS логов. Настраиваю alerts для ошибок и проблем с производительностью. Реализую логирование на разных уровнях (info, warn, error). Есть on-call ротация и процедуры реагирования на инциденты.
</details>

## Estimation

<details>
<summary><b>Как вы оцениваете задачи?</b></summary>

Разбиваю задачу на меньшие части, учитываю: время разработки, тестирование, code review, потенциальные blockers. Использую story points или часы. Учитываю сложность и неизвестные факторы. Сравниваю с похожими прошлыми задачами. Добавляю буфер на непредвиденные проблемы (обычно 20-30%). Обсуждаю с командой при неуверенности.
</details>

## Архитектура (Clean, Hexagonal, Onion)

<details>
<summary><b>Что такое Clean Architecture?</b></summary>

Слои разделены правилом зависимостей — внутренние слои не знают о внешних. Entities (ядро бизнеса) → Use Cases → Controllers/Presenters → External (DB, UI). Делает код тестируемым и независимым от фреймворков.
</details>

<details>
<summary><b>Что такое Hexagonal Architecture?</b></summary>

Также называется "Ports and Adapters". Ядро бизнес-логики в центре, взаимодействует с внешним миром через ports (интерфейсы) и adapters (реализации). Легко заменять базы данных, UI, внешние сервисы без изменения ядра логики.
</details>

<details>
<summary><b>Что такое Onion Architecture?</b></summary>

Похожа на Clean Architecture. Слои как луковица — Domain Model в центре, затем Domain Services, затем Application Services, затем Infrastructure. Зависимости направлены внутрь. Ядро не зависит от внешних concerns.
</details>

## Производительность приложения

<details>
<summary><b>Какие модели производительности приложений вы знаете?</b></summary>

Ключевые метрики: Time to First Byte (TTFB), First Contentful Paint (FCP), Largest Contentful Paint (LCP), Time to Interactive (TTI), Cumulative Layout Shift (CLS). Модели: RAIL (Response, Animation, Idle, Load) от Google — response <100ms, анимации 60fps, idle work <50ms, load <1s.
</details>

<details>
<summary><b>Как вы оптимизируете производительность приложения?</b></summary>

Frontend: code splitting, lazy loading, оптимизация изображений, кэширование, минификация, tree shaking, CDN. Уменьшение размера bundle. Избегание лишних re-renders (React.memo, useMemo). Backend: индексация базы данных, оптимизация запросов, кэширование (Redis), пагинация. Сначала профилирование, потом оптимизация узких мест.
</details>

## Test Pyramid

<details>
<summary><b>Объясните Test Pyramid и как вы применяете её в проектах</b></summary>

Форма пирамиды — больше тестов внизу, меньше наверху:
- **Unit-тесты** (низ): Много, быстрые, тестируют отдельные функции/компоненты
- **Integration-тесты** (середина): Тестируют взаимодействие модулей
- **E2E-тесты** (верх): Мало, медленные, тестируют полные пользовательские сценарии

Применяю, написывая много unit-тестов, несколько integration-тестов, мало E2E-тестов для критических путей. Быстрый feedback loop — ключевой фактор.
</details>

## React Experimental Features

<details>
<summary><b>Что такое компонент Activity в React?</b></summary>

`<Activity>` — экспериментальный компонент для управления жизненным циклом на основе приоритетов. Позволяет скрывать/показывать части UI, сохраняя их state.

**Ключевые возможности:**
- `mode="hidden"` — компонент скрыт, но state сохраняется
- `mode="visible"` — компонент отображается нормально
- Пониженный приоритет для скрытых компонентов — React может откладывать их обновления

```jsx
import { Activity } from 'react';

function App() {
  const [activeTab, setActiveTab] = useState('home');

  return (
    <>
      <Activity mode={activeTab === 'home' ? 'visible' : 'hidden'}>
        <HomePage />
      </Activity>
      <Activity mode={activeTab === 'profile' ? 'visible' : 'hidden'}>
        <ProfilePage />
      </Activity>
    </>
  );
}
```

**Сценарии использования:**
- Навигация по табам без потери state
- Offscreen prerendering
- Сохранение состояния форм при переключении views

Примечание: Это экспериментальная фича, может измениться до стабильного релиза.
</details>

<details>
<summary><b>Что такое хук useEffectEvent и какую проблему он решает?</b></summary>

`useEffectEvent` решает проблему "устаревших замыканий" в массиве зависимостей useEffect. Создаёт стабильную функцию с доступом к актуальным значениям без добавления в зависимости.

**Проблема, которую решает:**
```jsx
// Проблема: нужно добавить onTick в deps, но он меняется каждый рендер
function Timer({ onTick, interval }) {
  useEffect(() => {
    const id = setInterval(() => onTick(), interval);
    return () => clearInterval(id);
  }, [onTick, interval]); // onTick вызывает лишние перезапуски
}
```

**Решение с useEffectEvent:**
```jsx
import { useEffectEvent } from 'react';

function Timer({ onTick, interval }) {
  const tick = useEffectEvent(() => {
    onTick(); // Всегда имеет актуальный onTick
  });

  useEffect(() => {
    const id = setInterval(tick, interval);
    return () => clearInterval(id);
  }, [interval]); // tick стабильный, не нужен в deps
}
```

**Ключевые моменты:**
- Функция из useEffectEvent стабильна (та же ссылка)
- Всегда читает последние props/state при вызове
- Не должна вызываться во время рендера
- Использовать только внутри useEffect

Примечание: Сейчас экспериментальный, используйте с осторожностью.
</details>

<details>
<summary><b>Что такое cacheSignal API в React Server Components?</b></summary>

`cacheSignal` — экспериментальный API для управления инвалидацией кэша в React Server Components. Предоставляет сигнал для отмены кэшированных операций при очистке кэша.

**Базовое использование:**
```jsx
import { unstable_cacheSignal as cacheSignal } from 'react';
import { cache } from 'react';

const fetchData = cache(async (id) => {
  const signal = cacheSignal();

  const response = await fetch(`/api/data/${id}`, {
    signal // Отменить если кэш инвалидирован
  });

  return response.json();
});
```

**Почему это важно:**
- Предотвращает завершение устаревших запросов после очистки кэша
- Экономит ресурсы, отменяя ненужные fetches
- Работает с любым API, поддерживающим AbortSignal

**Сценарии использования:**
- Долгие серверные запросы данных
- Отмена устаревших запросов при навигации
- Очистка ресурсов при инвалидации кэша

Примечание: Это экспериментальный API с префиксом `unstable_`. API может измениться.
</details>
