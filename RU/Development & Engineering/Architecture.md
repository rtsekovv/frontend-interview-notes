# Вопросы для собеседования по Architecture

## Module Design

<details>
<summary><b>Как вы участвуете в создании дизайна модуля и/или его компонентов?</b></summary>

Анализирую требования, определяю ответственности и границы. Создаю диаграммы компонентов. Определяю интерфейсы между модулями. Учитываю: single responsibility, low coupling, high cohesion. Review с командой, итерации на основе feedback.
</details>

<details>
<summary><b>Опишите ваш опыт создания и предложения дизайна системы/модуля</b></summary>

(Личный вопрос — опишите: сбор требований, создание диаграмм, презентация команде, обработка feedback, рассмотренные trade-offs, используемые инструменты типа Miro, draw.io, формат документации.)
</details>

## Техническая документация

<details>
<summary><b>Как вы готовите техническую документацию?</b></summary>

Включайте: обзор архитектуры, описания компонентов, диаграммы потоков данных, API документацию, инструкции по настройке, гайд по деплою. Используйте понятный язык, диаграммы, примеры кода. Поддерживайте актуальность. Инструменты: Confluence, Notion, README files, JSDoc.
</details>

## Performance и Security

<details>
<summary><b>Как вы решаете проблемы производительности и безопасности?</b></summary>

Performance: профилируйте для поиска узких мест, измеряйте до/после, используйте инструменты мониторинга. Распространённые фиксы: кэширование, lazy loading, оптимизация базы данных. Security: следуйте OWASP guidelines, аудит зависимостей, валидация input, безопасная аутентификация. Регулярные security reviews.
</details>

## Architectural Patterns

<details>
<summary><b>Что такое Retry pattern и когда его использовать?</b></summary>

Автоматический повтор failed операций (сетевые вызовы, база данных). Используйте для transient failures. Реализуйте: max retries, exponential backoff, timeout limits. Не используйте для: ошибок валидации, permanent failures. Рассмотрите circuit breaker для повторяющихся failures.
</details>

<details>
<summary><b>Что такое Health Endpoint Monitoring pattern?</b></summary>

Выставляйте endpoint (например, `/health`), возвращающий статус сервиса. Проверяйте: зависимости (база данных, внешние сервисы), память, диск. Используется: load balancers, orchestrators (Kubernetes), системы мониторинга. Возвращайте 200 если здоров, 503 если нет.
</details>

<details>
<summary><b>Какие архитектурные подходы вы знаете?</b></summary>

- **Monolith**: Единый deployable unit, проще, хорош для небольших приложений
- **Microservices**: Независимые сервисы, масштабируемые, сложные
- **Serverless**: Functions as a service, без управления серверами
- **Event-driven**: Компоненты общаются через события
- **Layered**: Presentation → Business → Data слои
</details>

## Solution Design

<details>
<summary><b>Как вы объясняете pros и cons предлагаемых решений?</b></summary>

Структура: кратко опишите решение, перечислите pros (преимущества, соответствие требованиям), перечислите cons (риски, сложность, стоимость). Сравните с альтернативами. Используйте визуальные материалы. Будьте объективны, признавайте trade-offs. Дайте stakeholders принять informed decision.
</details>

<details>
<summary><b>Как вы предоставляете несколько возможных решений для engineering проблемы?</b></summary>

Сначала анализируйте проблему. Исследуйте существующие решения. Предложите 2-3 варианта с разными trade-offs (например, простое vs масштабируемое, быстрое vs дешёвое). Для каждого: опишите подход, estimate effort, pros/cons. Рекомендуйте одно с обоснованием.
</details>

<details>
<summary><b>Как вы решаете какое решение лучше и почему?</b></summary>

Оценивайте по критериям: соответствует требованиям, экспертиза команды, ограничения времени/бюджета, поддерживаемость, потребности в масштабировании, технический долг. При необходимости используйте weighted scoring. Учитывайте долгосрочное влияние. Получите input команды.
</details>

## Design Patterns в Architecture

<details>
<summary><b>Как вы описываете design patterns и архитектуру, используемые в проекте?</b></summary>

Документируйте: общий архитектурный стиль (monolith, microservices), структуру папок, основные используемые паттерны (MVC, Repository, Factory), flow данных, ключевые дизайн-решения и почему. Включайте диаграммы. Держите доступным для новых членов команды.
</details>

## Domain-Driven Design (DDD)

<details>
<summary><b>Что такое DDD (Domain-Driven Design)?</b></summary>

Подход с фокусом на core business domain. Ключевые концепции: Ubiquitous Language (общий словарь), Bounded Contexts (чёткие границы), Entities (идентичность), Value Objects (без идентичности), Aggregates (граница консистентности), Domain Events. Полезен для сложной бизнес-логики.
</details>

## Clean Code Principles (DRY, YAGNI, KISS)

<details>
<summary><b>Что такое принципы DRY, YAGNI и KISS?</b></summary>

**DRY — Don't Repeat Yourself**
- Избегайте дублирования кода
- Извлекайте повторяющуюся логику в переиспользуемые функции/компоненты
- Anti-pattern: Copy-paste похожих блоков кода

**YAGNI — You Aren't Gonna Need It**
- Не реализуйте функциональность пока она реально не нужна
- Anti-pattern: Добавление фич "на будущее", создание универсальных решений без требований
- Почему плохо: Усложняет код, замедляет разработку, увеличивает количество багов

**KISS — Keep It Simple, Stupid**
- Предпочитайте простейшее решение, которое работает
- Простота > "умность"
- Код читается чаще, чем пишется

| Принцип | Защищает от |
|---------|-------------|
| DRY | Дублирования |
| YAGNI | Преждевременной сложности |
| KISS | Over-architecture |

**Ответ для собеседования:** DRY, YAGNI и KISS — фундаментальные принципы clean code. DRY уменьшает дублирование, YAGNI защищает от преждевременной реализации ненужных фич, KISS сохраняет решения простыми и поддерживаемыми. Ключ — применять их прагматично, а не догматично.
</details>

## MVC (Model-View-Controller)

<details>
<summary><b>Что такое MVC pattern?</b></summary>

MVC — архитектурный паттерн, разделяющий приложение на три ответственности:
- **Model** — данные и бизнес-логика, ничего не знает о UI
- **View** — отображение данных (UI)
- **Controller** — обрабатывает действия пользователя, координирует Model и View

**Data flow:** User → Controller → Model → View

**Зачем использовать MVC:**
- Separation of concerns (SoC)
- Улучшенная тестируемость
- Проще поддерживать
- Хорош для больших приложений

**MVC в современном frontend:**
Классический MVC редко используется напрямую во frontend сегодня. View и Controller часто переплетаются, сам DOM является "View".

| MVC | React |
|-----|-------|
| Model | State |
| View | JSX / Template |
| Controller | Component / Hooks |

Часто называют **MV*** вместо строгого MVC.

**Pros:** Чёткое разделение, переиспользуемость, хорош для серверных приложений

**Cons:** Сложен для UI-heavy приложений, Controller может разрастись, не идеален для высоко интерактивных SPA

**Ответ для собеседования:** MVC — архитектурный паттерн, разделяющий Model, View и Controller для изоляции бизнес-логики от представления и действий пользователя, улучшая поддерживаемость и тестируемость.
</details>

## Clean, Hexagonal и Onion Architecture

<details>
<summary><b>Что такое Clean/Hexagonal/Onion Architecture?</b></summary>

Все три — вариации одной идеи: **бизнес-логика должна быть независима от UI, фреймворков, БД и инфраструктуры**. Они различаются терминологией и визуальной моделью, но философия одна.

---

**1. Clean Architecture (Robert C. Martin)**

Разделяет систему на слои со строгим правилом зависимостей: **зависимости всегда направлены внутрь**, к бизнес-логике.

Слои (изнутри → наружу):
1. **Entities** — бизнес-правила, доменные модели
2. **Use Cases** — бизнес-сценарии, логика приложения
3. **Interface Adapters** — controllers, presenters, gateways
4. **Frameworks & Drivers** — UI (React), API, DB, сторонние библиотеки

---

**2. Hexagonal Architecture (Ports & Adapters)**

Фокусируется на **взаимодействии системы с внешним миром**. Приложение в центре, всё остальное подключается через **ports и adapters**.

- **Ports** — интерфейсы, контракты (что система ожидает)
- **Adapters** — реализации (API, UI, DB, WebSocket)

Flow: `UI/API/Tests → Adapter → Port → Application Core`

---

**3. Onion Architecture**

Визуально подчёркивает **слоистость и инверсию зависимостей**. Более глубокий слой = более стабильный и независимый.

Слои: Domain → Domain Services → Application Services → Infrastructure → UI

Правило: Внешние слои зависят от внутренних, внутренние ничего не знают о внешних.

---

**Сравнение:**

| Аспект | Clean | Hexagonal | Onion |
|--------|-------|-----------|-------|
| Фокус | Бизнес-правила | Внешнее взаимодействие | Слоистость |
| Термины | Use Cases | Ports / Adapters | Domain |
| Зависимости | Внутрь | Через ports | Внутрь |
| Особенность | Формализация | Гибкость | Визуальная модель |

**Frontend примеры:**
- Use cases → `placeBet()`
- Entities → `Bet`, `Odds`
- Port → `OddsProvider` interface
- Adapter → REST / SSE / WebSocket реализация
- UI (React) → просто вызывает use cases

**Pros:** Тестируемость, слабая связанность, независимость от фреймворков, готовность к изменениям

**Cons:** Overengineering для маленьких проектов, больше кода и абстракций, требует зрелой команды

**Ответ для собеседования:** Clean, Hexagonal и Onion Architecture разделяют одну цель: изолировать бизнес-логику от UI и инфраструктуры с зависимостями, направленными внутрь. Они различаются терминологией, но обеспечивают высокую тестируемость, расширяемость и независимость от фреймворков.
</details>

## Dependency Inversion vs Dependency Injection

<details>
<summary><b>В чём разница между Dependency Inversion (DIP) и Dependency Injection (DI)?</b></summary>

**Dependency Inversion Principle (DIP)** — принцип SOLID:
- High-level модули не должны зависеть от low-level модулей
- Оба должны зависеть от абстракций
- Абстракции не должны зависеть от деталей

**Dependency Injection (DI)** — техника для реализации DIP:
- Зависимости передаются (инжектятся) извне, а не создаются внутри
- DI — способ достижения Dependency Inversion

**Без DI (tight coupling):**
```javascript
class UserService {
  constructor() {
    this.api = new ApiService(); // Жёсткая зависимость
  }
}
```

**С DI (loose coupling):**
```javascript
class UserService {
  constructor(api) {
    this.api = api; // Зависимость инжектирована
  }
}
const userService = new UserService(new ApiService());
```

**DI во Frontend Frameworks:**
- **React**: Props, Context API
- **Angular**: Встроенный DI container (`@Injectable()`)
- **Vue**: `provide` / `inject`

| Аспект | DIP | DI |
|--------|-----|-----|
| Тип | Принцип | Техника |
| Фокус | Как модули должны зависеть | Как передавать зависимости |
| Уровень | Архитектурный | Реализация |

**Ответ для собеседования:** DIP — принцип, что модули должны зависеть от абстракций; DI — техника передачи зависимостей извне для достижения слабой связанности и тестируемости.
</details>

## Frontend System Design

<details>
<summary><b>Спроектируйте онлайн редактор кода типа StackBlitz (frontend system design)</b></summary>

**Основные требования:**
- Файловая система с древовидной навигацией
- Редактирование нескольких файлов с подсветкой синтаксиса
- Live preview/выполнение
- Real-time коллаборация (опционально)

**Архитектура:**

```
┌─────────────────────────────────────────────────────────┐
│                      App Shell                          │
├──────────┬──────────────────────┬──────────────────────┤
│  File    │     Code Editor      │   Preview Panel      │
│  Tree    │     (Monaco/CM)      │   (iframe/WebContainer)│
├──────────┴──────────────────────┴──────────────────────┤
│              Virtual File System (IndexedDB)           │
├────────────────────────────────────────────────────────┤
│         Bundler (esbuild-wasm / WebContainer)          │
└────────────────────────────────────────────────────────┘
```

**Ключевые компоненты:**

1. **Редактор кода:**
   - Использовать Monaco Editor (движок VS Code) или CodeMirror
   - Фичи: подсветка синтаксиса, автодополнение, multi-cursor

2. **Виртуальная файловая система:**
   - In-memory file tree с persistence в IndexedDB
   - Файловые операции: create, read, update, delete, rename
   - Watch изменений и trigger rebuilds

3. **Bundler/Transpiler:**
   - Вариант A: esbuild-wasm для bundling в браузере
   - Вариант B: WebContainer (технология StackBlitz) — Node.js в браузере
   - Обработка npm-зависимостей через esm.sh или Skypack CDN

4. **Preview Panel:**
   - Sandboxed iframe с srcdoc или blob URL
   - Hot Module Replacement для instant-обновлений
   - Error boundary для runtime-ошибок

**State management:**
```typescript
interface EditorState {
  files: Map<string, FileNode>;
  openTabs: string[];
  activeFile: string;
  unsavedChanges: Set<string>;
}
```

**Соображения по производительности:**
- Debounce компиляции при нажатии клавиш
- Web Workers для тяжёлых операций (parsing, bundling)
- Виртуальный скролл для больших файлов
- Lazy load фич редактора
</details>

<details>
<summary><b>Спроектируйте систему уведомлений с offline-поддержкой</b></summary>

**Требования:**
- Real-time push-уведомления
- Центр уведомлений с историей
- Offline-хранение и синхронизация
- Статус прочитано/непрочитано между устройствами

**Архитектура:**

```
┌──────────────────────────────────────────────────────┐
│                    Frontend                           │
├──────────────────────────────────────────────────────┤
│  Notification │  Service Worker  │  IndexedDB Cache  │
│  Center UI    │  (Push + Sync)   │  (Offline Store)  │
├──────────────────────────────────────────────────────┤
│              Notification Manager                     │
│  - Управление очередью                               │
│  - Дедупликация                                       │
│  - Обработка приоритетов                             │
└──────────────────────────────────────────────────────┘
              │
              │ WebSocket / Server-Sent Events
              ▼
┌──────────────────────────────────────────────────────┐
│                    Backend                            │
│  Notification Service → Message Queue → Push Service │
└──────────────────────────────────────────────────────┘
```

**Реализация:**

```typescript
class NotificationManager {
  private db: IDBDatabase;
  private wsConnection: WebSocket;
  private pendingSync: Notification[] = [];

  async initialize() {
    this.db = await this.openDB();
    this.setupServiceWorker();
    this.connectWebSocket();
    this.syncPendingActions();
  }

  async addNotification(notification: Notification) {
    // Сначала сохраняем локально (offline-first)
    await this.storeLocal(notification);
    // Обновляем UI
    this.emit('notification', notification);
    // Показываем системное уведомление если разрешено
    if (notification.showPush) {
      this.showPushNotification(notification);
    }
  }

  async markAsRead(id: string) {
    // Обновляем локальное состояние
    await this.updateLocal(id, { read: true, readAt: Date.now() });

    // Ставим в очередь sync если offline
    if (!navigator.onLine) {
      this.pendingSync.push({ action: 'markRead', id });
      return;
    }

    // Синхронизируем с сервером
    await this.syncWithServer({ action: 'markRead', id });
  }
}
```

**Стратегия offline sync:**
- Храним все уведомления в IndexedDB
- Отслеживаем pending actions (read, dismiss)
- Background Sync API для отложенной синхронизации с сервером
- Разрешение конфликтов: last-write-wins с timestamps
</details>

<details>
<summary><b>Постройте micro-frontend архитектуру для крупного enterprise-приложения</b></summary>

**Когда использовать micro-frontends:**
- Несколько команд работают над одним продуктом
- Нужен независимый деплой фич
- Модернизация legacy (постепенная миграция)
- Разные требования к tech stack

**Подходы к интеграции:**

1. **Build-time интеграция (Module Federation):**
```javascript
// webpack.config.js — Host app
new ModuleFederationPlugin({
  name: 'host',
  remotes: {
    dashboard: 'dashboard@http://localhost:3001/remoteEntry.js',
    settings: 'settings@http://localhost:3002/remoteEntry.js',
  },
  shared: ['react', 'react-dom'],
});

// Использование в host
const Dashboard = React.lazy(() => import('dashboard/App'));
```

2. **Runtime интеграция (Single-SPA):**
```javascript
// root-config.js
registerApplication({
  name: '@org/dashboard',
  app: () => System.import('@org/dashboard'),
  activeWhen: ['/dashboard'],
});

start();
```

**Общие concerns:**

```
┌─────────────────────────────────────────────────────────┐
│                    Shell / Host App                      │
│  - Routing                                               │
│  - Authentication                                        │
│  - Shared UI (Header, Navigation)                        │
├──────────┬──────────┬──────────┬────────────────────────┤
│  MFE 1   │  MFE 2   │  MFE 3   │        MFE N           │
│ (React)  │  (Vue)   │ (React)  │      (Angular)         │
├──────────┴──────────┴──────────┴────────────────────────┤
│              Shared Dependencies Layer                   │
│  - Design System                                         │
│  - Authentication SDK                                    │
│  - Analytics                                             │
│  - Event Bus                                             │
└─────────────────────────────────────────────────────────┘
```

**Коммуникация между MFEs:**
```typescript
// Custom events
window.dispatchEvent(new CustomEvent('user:updated', { detail: user }));
window.addEventListener('user:updated', (e) => handleUserUpdate(e.detail));
```

**Challenges и решения:**
- **Консистентные стили**: Shared design system как npm package
- **Shared state**: Event bus или shared store (Redux с namespacing)
- **Routing**: Централизованный router в shell, MFEs обрабатывают sub-routes
- **Performance**: Shared dependencies, lazy loading MFEs
</details>

<details>
<summary><b>Как защитить frontend routes + токены в реальном приложении?</b></summary>

**Защита роутов:**
```typescript
function ProtectedRoute({ children, requiredRoles }) {
  const { user, isLoading } = useAuth();

  if (isLoading) return <LoadingSpinner />;

  if (!user) {
    return <Navigate to="/login" state={{ from: location }} />;
  }

  if (requiredRoles && !requiredRoles.some(role => user.roles.includes(role))) {
    return <Navigate to="/unauthorized" />;
  }

  return children;
}

// Использование
<Route path="/admin" element={
  <ProtectedRoute requiredRoles={['admin']}>
    <AdminDashboard />
  </ProtectedRoute>
} />
```

**Управление токенами:**

```typescript
class TokenManager {
  // Access token — короткоживущий, хранится в памяти
  private accessToken: string | null = null;

  // Refresh token — httpOnly cookie (устанавливается сервером)
  // Недоступен для JavaScript = защита от XSS

  setAccessToken(token: string) {
    this.accessToken = token;
  }

  async refreshAccessToken() {
    // Cookie автоматически отправляется
    const response = await fetch('/api/auth/refresh', {
      method: 'POST',
      credentials: 'include', // Включаем cookies
    });

    if (!response.ok) {
      this.accessToken = null;
      throw new Error('Session expired');
    }

    const { accessToken } = await response.json();
    this.accessToken = accessToken;
    return accessToken;
  }
}
```

**Best practices безопасности:**
1. **Никогда не храните токены в localStorage** — уязвимо к XSS
2. **Используйте httpOnly cookies для refresh tokens** — недоступны для JS
3. **Короткоживущие access tokens** (5-15 минут)
4. **Реализуйте CSRF-защиту** для cookie-based auth
5. **Валидируйте на сервере** — frontend проверки только для UX
</details>

<details>
<summary><b>Спроектируйте real-time dashboard с графиками и потоковыми данными</b></summary>

**Требования:**
- Real-time обновления данных (1-5 секунд интервалы)
- Несколько типов графиков (line, bar, pie)
- Производительность с тысячами точек данных
- Graceful handling проблем соединения

**Архитектура:**

```
┌─────────────────────────────────────────────────────────┐
│                    Dashboard UI                          │
├────────────┬────────────┬────────────┬─────────────────┤
│  Chart 1   │  Chart 2   │  Chart 3   │    Widgets      │
│  (Metrics) │  (Trends)  │   (Pie)    │   (KPIs)        │
├────────────┴────────────┴────────────┴─────────────────┤
│              Data Management Layer                       │
│  - Subscription Manager                                  │
│  - Data Aggregation                                      │
│  - Buffer Management                                     │
├─────────────────────────────────────────────────────────┤
│         WebSocket / SSE Connection Manager              │
└─────────────────────────────────────────────────────────┘
```

**Обработка real-time данных:**

```typescript
class DashboardDataManager {
  private ws: WebSocket;
  private buffer: Map<string, DataPoint[]> = new Map();
  private subscribers: Map<string, Set<Callback>> = new Map();
  private maxBufferSize = 1000;

  connect() {
    this.ws = new WebSocket('wss://api.example.com/stream');

    this.ws.onmessage = (event) => {
      const data = JSON.parse(event.data);
      this.processData(data);
    };

    this.ws.onclose = () => {
      // Reconnect с exponential backoff
      setTimeout(() => this.connect(), this.getBackoffDelay());
    };
  }

  subscribe(metric: string, callback: Callback) {
    if (!this.subscribers.has(metric)) {
      this.subscribers.set(metric, new Set());
    }
    this.subscribers.get(metric)!.add(callback);

    // Возвращаем функцию отписки
    return () => this.subscribers.get(metric)?.delete(callback);
  }
}
```

**Оптимизация графиков:**
- Используйте canvas-based графики (Chart.js, ECharts)
- Batch DOM-обновления через requestAnimationFrame
- Downsample данные для отображения (храните полные для зуминга)
- Web Workers для обработки данных
- Throttle/debounce UI-обновления (max 30-60 fps)
</details>

## Масштабируемость и качество кода

<details>
<summary><b>Как структурировать большое React-приложение?</b></summary>

Feature-based структура (не по типам файлов):
```
src/
  features/
    auth/
      components/
      hooks/
      api/
      types/
    dashboard/
      ...
  shared/
    components/
    hooks/
    utils/
  app/
    routes.tsx
    store.ts
```
Каждая feature самодостаточна. Shared папка для общих утилит. Чёткие правила импортов между features.
</details>

<details>
<summary><b>Где размещать бизнес-логику в React-приложении?</b></summary>

- **Custom hooks**: Для переиспользуемой stateful логики
- **Services/utils**: Для чистой бизнес-логики без React-зависимостей
- **State managers**: Для сложных трансформаций состояния
- **НЕ в компонентах**: Компоненты должны быть тонкими, фокус на рендеринге

Держите компоненты "глупыми", логику в выделенных слоях. Проще тестировать и поддерживать.
</details>

<details>
<summary><b>Как обрабатывать cross-cutting concerns?</b></summary>

Cross-cutting: логирование, auth, обработка ошибок, аналитика. Решения:
- **Higher-Order Components**: Оборачивают компоненты общей логикой
- **Custom hooks**: Шарят логику между компонентами
- **Context**: Предоставляет глобальную функциональность
- **Middleware**: Для actions state management
- **Aspect-oriented паттерны**: Декораторы, интерсепторы
</details>

<details>
<summary><b>Как справляться с техническим долгом?</b></summary>

1. **Отслеживайте**: Документируйте в backlog с impact/effort
2. **Выделяйте время**: 10-20% спринта на сокращение долга
3. **Приоритизируйте**: Сначала исправляйте high-impact, low-effort
4. **Предотвращайте**: Code reviews, стандарты, автоматические проверки
5. **Рефакторите инкрементально**: Не ждите больших переписываний

Балансируйте новые фичи с поддержкой. Делайте долг видимым для stakeholders.
</details>

<details>
<summary><b>Как реализовать feature flags?</b></summary>

Feature flags контролируют доступность фич без изменения кода:
```javascript
if (featureFlags.newCheckout) {
  return <NewCheckout />;
}
return <OldCheckout />;
```
Используйте для: постепенного rollout, A/B тестирования, быстрого отката, trunk-based разработки.

Инструменты: LaunchDarkly, Unleash, кастомное решение с конфигом.
</details>

<details>
<summary><b>Какие coding standards вы используете?</b></summary>

- **Linting**: ESLint с согласованными командой правилами
- **Formatting**: Prettier для консистентности
- **Naming**: Понятные, описательные имена (без сокращений)
- **File structure**: Консистентная организация
- **TypeScript**: Strict mode, избегать `any`
- **Git**: Conventional commits, осмысленные сообщения

Автоматизируйте через pre-commit hooks. Документируйте в гайдах команды.
</details>

<details>
<summary><b>Что делает код читаемым?</b></summary>

- **Понятные названия**: Переменные и функции описывают своё назначение
- **Маленькие функции**: Единая ответственность, идеально 10-20 строк
- **Консистентный стиль**: Одинаковые паттерны по всей кодовой базе
- **Осмысленные абстракции**: Правильный уровень абстракции
- **Комментарии когда нужно**: Объясняйте "почему", не "что"
- **Тесты как документация**: Показывают как код должен использоваться

Код читают в 10 раз чаще, чем пишут. Оптимизируйте для чтения.
</details>
