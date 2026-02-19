# Вопросы для собеседования по General Development Skills

## Git и Git Flow

<details>
<summary><b>Объясните Git Flow branching model</b></summary>

Ветки: `main` (production), `develop` (интеграция), `feature/*` (новые фичи), `release/*` (подготовка релиза), `hotfix/*` (срочные исправления). Flow: создаём feature от develop → merge в develop → создаём release → merge в main и develop. Tags для версий.
</details>

## Environments

<details>
<summary><b>Какие бывают environments (dev, staging, production)?</b></summary>

- **Development**: Локальная машина, частые изменения, debug mode
- **Staging**: Похож на production, для QA-тестирования, безопасно ломать
- **Production**: Живые пользователи, стабильность, мониторинг, без debugging

У каждого свой config, база данных, API keys. CI/CD деплоит в каждый.
</details>

## HTTP/HTTPS

<details>
<summary><b>В чём разница между HTTP и HTTPS?</b></summary>

- **HTTP**: Незашифрованный, данные видны атакующим, порт 80
- **HTTPS**: Зашифрованный TLS/SSL, безопасный, порт 443, требует сертификат

Всегда используйте HTTPS для production. Обязателен для: паролей, платежей, cookies, SEO-преимуществ.
</details>

## Bash и терминал

<details>
<summary><b>Какие базовые Bash-команды вы используете ежедневно?</b></summary>

Навигация: `cd`, `ls`, `pwd`. Файлы: `cat`, `mkdir`, `rm`, `cp`, `mv`. Git: `git status/add/commit/push/pull`. npm: `npm install/run/test`. Поиск: `grep`, `find`. Другие: `curl`, `chmod`, `ps`, `kill`.
</details>

## Docker

<details>
<summary><b>Что такое Docker? Объясните image, container, volume, registry</b></summary>

- **Docker**: Платформа для контейнеризированных приложений
- **Image**: Blueprint/шаблон, read-only, содержит приложение и зависимости
- **Container**: Работающий экземпляр image, изолированное окружение
- **Volume**: Постоянное хранилище, сохраняется при рестарте container
- **Registry**: Репозиторий images (Docker Hub, ECR)
</details>

<details>
<summary><b>Как писать Dockerfile?</b></summary>

```dockerfile
FROM node:18-alpine       # Базовый image
WORKDIR /app              # Устанавливаем рабочую директорию
COPY package*.json ./     # Копируем файлы зависимостей
RUN npm install           # Устанавливаем зависимости
COPY . .                  # Копируем исходный код
EXPOSE 3000               # Документируем порт
CMD ["npm", "start"]      # Команда запуска
```
</details>

## JWT

<details>
<summary><b>Что такое JWT и как он работает?</b></summary>

JSON Web Token — компактный, URL-safe токен для аутентификации. Три части: Header (алгоритм), Payload (claims/данные), Signature (проверка целостности). Сервер создаёт токен при логине, клиент отправляет в Authorization header. Сервер проверяет signature, хранение сессий не нужно.
</details>

## Hosting и Domains

<details>
<summary><b>Как настроить hosting и domains?</b></summary>

Domain: купите у регистратора (Namecheap, GoDaddy). Hosting: выберите провайдера (Vercel, AWS, DigitalOcean). Настройте DNS: A record (IP) или CNAME (domain). Настройте SSL сертификат (Let's Encrypt бесплатно). Настройте web server (nginx) или используйте platform defaults.
</details>

## CI/CD

<details>
<summary><b>Как настроить CI/CD pipelines?</b></summary>

Инструменты: GitHub Actions, GitLab CI, Jenkins. Настройка: создайте config file (`.github/workflows/`). Шаги: install deps → lint → test → build → deploy. Triggers: push, PR, schedule. Secrets для API keys. Deploy на staging при merge, на production при release.
</details>

## Качество кода (Linters и Formatters)

<details>
<summary><b>Какие code linters и formatters вы используете?</b></summary>

- **ESLint**: Ловит ошибки, обеспечивает правила
- **Prettier**: Авто-форматирование кода
- **TypeScript**: Проверка типов
- **Stylelint**: Линтинг CSS

Настройка: config files, интеграция в IDE, pre-commit hooks (husky + lint-staged).
</details>

## Dependency Inversion и Injection

<details>
<summary><b>Что такое принцип Dependency Inversion?</b></summary>

High-level модули не должны зависеть от low-level модулей. Оба должны зависеть от абстракций. Пример: сервис зависит от interface, а не от конкретного класса базы данных. Преимущества: проще тестирование, заменяемые реализации.
</details>

<details>
<summary><b>Что такое Dependency Injection и почему это полезно?</b></summary>

Передача зависимостей в компонент вместо создания внутри. Типы: constructor injection, setter injection, interface injection. Преимущества: слабая связанность, тестируемость (внедрение mocks), гибкость. Фреймворки: Angular имеет встроенный DI.
</details>

## Инфраструктура

<details>
<summary><b>Как настроить инфраструктуру проекта с нуля?</b></summary>

Шаги: выбор hosting (cloud/VPS), настройка server/container, настройка web server, настройка базы данных, настройка domains/SSL, настройка CI/CD, настройка monitoring/logging, environment variables, стратегия backup. Документируйте всё.
</details>

## Структуры данных

<details>
<summary><b>Какие структуры данных вы часто используете?</b></summary>

- **Array**: Упорядоченный список, быстрый доступ по индексу
- **Object/Map**: Key-value пары, быстрый lookup
- **Set**: Уникальные значения, быстрая проверка наличия
- **Stack**: LIFO (функционал undo)
- **Queue**: FIFO (обработка задач)
- **Tree**: DOM, файловые системы, иерархические данные
</details>

## Алгоритмы

<details>
<summary><b>Какие алгоритмы важны для frontend-разработки?</b></summary>

- **Searching**: Binary search (отсортированные данные)
- **Sorting**: Понимание встроенной сортировки
- **Debounce/Throttle**: Rate limiting
- **Memoization**: Кэширование результатов
- **Tree traversal**: DOM manipulation
- **Diffing**: Virtual DOM (алгоритм React)
</details>

## Debugging и производительность

<details>
<summary><b>Приложение загружается 8 секунд — как анализировать и исправить?</b></summary>

**Диагностический подход:**

1. **Сначала измеряем** (Lighthouse, WebPageTest, Chrome DevTools):
```
Performance tab → Record page load → Analyze waterfall
```

2. **Распространённые причины и решения:**

**Сетевые проблемы:**
- Большие размеры bundle → Code splitting, lazy loading
- Слишком много запросов → Bundle, sprite sheets, HTTP/2
- Медленный TTFB → CDN, серверная оптимизация, кэширование
- Нет сжатия → Включите gzip/brotli

**Проблемы JavaScript:**
```javascript
// Проверьте bundle analysis
npx webpack-bundle-analyzer stats.json

// Code splitting
const HeavyComponent = lazy(() => import('./Heavy'));
```

**Render blocking:**
```html
<!-- Перенесите скрипты вниз или используйте defer -->
<script src="app.js" defer></script>

<!-- Critical CSS inline, остальное async -->
<style>/* critical */</style>
<link rel="preload" href="styles.css" as="style" onload="this.rel='stylesheet'">
```

**Чеклист:**
- [ ] Анализ размера bundle (цель: <200KB gzipped для initial)
- [ ] Проверка render-blocking ресурсов
- [ ] Проверка caching headers
- [ ] Тест на throttled connection (3G)
- [ ] Проверка влияния сторонних скриптов
- [ ] Review Web Vitals (LCP, FID, CLS)
</details>

<details>
<summary><b>Случайный logout после refresh токена — как дебажить?</b></summary>

**Шаги исследования:**

1. **Добавьте comprehensive logging:**
```typescript
class AuthLogger {
  log(event: string, data?: any) {
    console.log(`[Auth ${new Date().toISOString()}] ${event}`, data);
    // Также отправляем в monitoring service
    analytics.track('auth_event', { event, ...data });
  }
}

// В flow refresh токена
authLogger.log('refresh_started', { tokenAge });
try {
  const newToken = await refreshToken();
  authLogger.log('refresh_success', { newTokenExpiry });
} catch (error) {
  authLogger.log('refresh_failed', { error: error.message, status: error.status });
}
```

2. **Распространённые причины:**

**Race conditions:**
```typescript
// Проблема: Несколько вкладок одновременно обновляют
// Решение: Используйте locks
const refreshLock = new Lock('token_refresh');

async function refreshTokenSafe() {
  if (await refreshLock.acquire()) {
    try {
      return await refreshToken();
    } finally {
      refreshLock.release();
    }
  }
  // Ждём refresh другой вкладки
  return waitForNewToken();
}
```

**Проблемы timing:**
```typescript
// Проблема: Токен истекает во время refresh-запроса
// Решение: Refresh заранее
const REFRESH_BUFFER = 60 * 1000; // За 1 минуту до истечения

function shouldRefresh(token) {
  const expiry = decodeToken(token).exp * 1000;
  return Date.now() > expiry - REFRESH_BUFFER;
}
```

**Проблемы с cookies:**
- Проверьте атрибут SameSite для cross-origin
- Проверьте флаг Secure для HTTPS
- Проверьте настройки domain/path
</details>

<details>
<summary><b>UI зависает при скролле — как профилировать и решить?</b></summary>

**Профилирование:**
```
Chrome DevTools → Performance tab → Record while scrolling
Ищите: Long tasks (>50ms), Layout thrashing, Excessive paints
```

**Распространённые причины и решения:**

1. **Слишком много DOM nodes:**
```javascript
// Проблема: Рендеринг 10000 элементов списка
// Решение: Виртуализация
import { FixedSizeList } from 'react-window';

<FixedSizeList height={600} itemCount={10000} itemSize={50}>
  {({ index, style }) => <Row style={style} data={items[index]} />}
</FixedSizeList>
```

2. **Layout thrashing:**
```javascript
// Плохо: Форсирует layout на каждой итерации
items.forEach(item => {
  const height = element.offsetHeight; // Read (форсирует layout)
  element.style.height = height + 10 + 'px'; // Write
});

// Хорошо: Batch reads и writes
const heights = items.map(() => element.offsetHeight); // Все reads
items.forEach((item, i) => {
  element.style.height = heights[i] + 10 + 'px'; // Все writes
});
```

3. **Тяжёлые scroll handlers:**
```javascript
// Плохо
window.addEventListener('scroll', () => {
  expensiveOperation();
});

// Хорошо: Throttle + RAF
let ticking = false;
window.addEventListener('scroll', () => {
  if (!ticking) {
    requestAnimationFrame(() => {
      expensiveOperation();
      ticking = false;
    });
    ticking = true;
  }
});
```

4. **CSS оптимизации:**
```css
/* Используйте will-change для анимируемых элементов */
.animated { will-change: transform; }

/* Используйте transform вместо top/left */
.moving { transform: translateY(100px); }

/* Используйте CSS containment */
.list-item { contain: layout style paint; }
```
</details>

<details>
<summary><b>Утечка памяти из-за subscriptions — как обнаружить и предотвратить?</b></summary>

**Обнаружение:**
```
Chrome DevTools → Memory tab → Take heap snapshot
→ Выполните операции → Сделайте ещё snapshot
→ Сравните: Ищите растущие detached DOM nodes, event listeners
```

**Распространённые причины:**

1. **Неочищенные subscriptions:**
```javascript
// Плохо: Утечка памяти
useEffect(() => {
  const subscription = eventEmitter.subscribe(handler);
  // Нет cleanup!
}, []);

// Хорошо: Cleanup
useEffect(() => {
  const subscription = eventEmitter.subscribe(handler);
  return () => subscription.unsubscribe();
}, []);
```

2. **Event listeners не удалены:**
```javascript
// Плохо
useEffect(() => {
  window.addEventListener('resize', handleResize);
}, []);

// Хорошо
useEffect(() => {
  window.addEventListener('resize', handleResize);
  return () => window.removeEventListener('resize', handleResize);
}, []);
```

3. **Таймеры не очищены:**
```javascript
useEffect(() => {
  const intervalId = setInterval(poll, 5000);
  return () => clearInterval(intervalId);
}, []);
```

**Паттерны предотвращения:**

```typescript
// AbortController для fetch
useEffect(() => {
  const controller = new AbortController();

  fetch('/api/data', { signal: controller.signal })
    .then(setData);

  return () => controller.abort();
}, []);

// RxJS subscriptions
useEffect(() => {
  const sub = observable$.subscribe(handler);
  return () => sub.unsubscribe();
}, []);
```
</details>

<details>
<summary><b>Периодические API failures только в production — стратегия отладки</b></summary>

**Систематический подход:**

1. **Добавьте observability:**
```typescript
async function apiCall(endpoint, options) {
  const requestId = generateId();
  const startTime = Date.now();

  logger.info('api_request', {
    requestId,
    endpoint,
    method: options.method,
    timestamp: startTime,
  });

  try {
    const response = await fetch(endpoint, options);
    const duration = Date.now() - startTime;

    logger.info('api_response', {
      requestId,
      status: response.status,
      duration,
    });

    return response;
  } catch (error) {
    logger.error('api_error', {
      requestId,
      error: error.message,
      duration: Date.now() - startTime,
    });
    throw error;
  }
}
```

2. **Проверьте различия окружений:**
- CORS конфигурация (разные домены)
- SSL/TLS certificate issues
- CDN caching behavior
- Load balancer timeout settings
- Rate limiting / throttling

3. **Сетевые issues:**
```typescript
// Определяем условия сети
navigator.connection?.addEventListener('change', () => {
  logger.info('network_change', {
    effectiveType: navigator.connection.effectiveType,
    downlink: navigator.connection.downlink,
  });
});

// Retry с jitter
async function fetchWithRetry(url, options, maxRetries = 3) {
  for (let i = 0; i < maxRetries; i++) {
    try {
      return await fetch(url, options);
    } catch (error) {
      if (i === maxRetries - 1) throw error;

      const delay = Math.min(1000 * Math.pow(2, i), 10000);
      const jitter = Math.random() * 1000;
      await sleep(delay + jitter);
    }
  }
}
```

4. **Используйте error tracking service:**
- Sentry, Bugsnag или Datadog
- Отслеживайте частоту ошибок, влияние на пользователей, stack traces
- Настройте alerts для всплесков error rate

**Типичные production-only issues:**
- DNS resolution failures
- Certificate pinning issues
- Geographic-specific routing problems
- Peak traffic timing issues
- Деградация сторонних сервисов
</details>
