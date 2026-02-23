# Вопросы для собеседования по React

## Create React App и настройка

<details>
<summary><b>Как использовать CRA и какие преимущества он даёт?</b></summary>

Запустите `npx create-react-app my-app`. Преимущества: нулевая конфигурация, webpack/babel предварительно настроены, hot reloading, настройка тестирования, оптимизированная production-сборка. Хорошо для обучения и small-medium проектов.
</details>

<details>
<summary><b>Какие преимущества использования Create React App для старта React-проекта по сравнению с настройкой с нуля?</b></summary>

Не нужна конфигурация webpack/babel, best practices встроены, лёгкие обновления через react-scripts, включены инструменты тестирования (Jest), консистентная структура проекта, быстрый старт. Ручная настройка даёт больше контроля, но требует времени.
</details>

<details>
<summary><b>Как React обрабатывает события?</b></summary>

React использует SyntheticEvents — обёртку над нативными событиями для кроссбраузерной совместимости. Именование в camelCase (`onClick`). Передавайте ссылку на функцию, а не вызов (`onClick={handleClick}`, не `onClick={handleClick()}`). События пулятся для производительности.
</details>

<details>
<summary><b>Какие сложности или ограничения при использовании Create React App?</b></summary>

Ограниченная кастомизация без eject, нет поддержки SSR, нельзя изменить webpack напрямую, может включать неиспользуемый код, eject необратим. Альтернативы: Next.js, Vite, кастомная настройка.
</details>

## Архитектура и структура проекта

<details>
<summary><b>Объясните концепцию компонентной архитектуры в React</b></summary>

UI строится из переиспользуемых, независимых компонентов. Каждый компонент управляет своим рендерингом и логикой. Компоненты компонуются в более крупные компоненты. Преимущества: переиспользуемость, изоляция, упрощённое тестирование, параллельная разработка.
</details>

<details>
<summary><b>Как вы обычно организуете структуру папок в React-проекте?</b></summary>

Распространённая структура:
- `src/`: Весь исходный код
- `components/`: Переиспользуемые UI-компоненты
- `pages/` или `views/`: Компоненты уровня роутов
- `hooks/`: Кастомные hooks
- `utils/`: Вспомогательные функции
- `services/`: API-вызовы
- `context/` или `store/`: Управление состоянием
</details>

<details>
<summary><b>Какие подходы вы используете при разработке архитектуры приложения?</b></summary>

Учитывайте: разделение ответственности, иерархию компонентов, стратегию управления состоянием, структуру папок (по фичам vs по типам), подход к стилям, стратегию тестирования. Документируйте решения. Начинайте просто, рефакторите по мере необходимости.
</details>

<details>
<summary><b>Какие преимущества Fractal-архитектуры?</b></summary>

Каждая папка фичи содержит всё необходимое (компоненты, hooks, тесты, стили). Самодостаточные модули. Преимущества: легко найти связанный код, переносимые фичи, хорошо масштабируется, чёткие границы.
</details>

<details>
<summary><b>Какие преимущества Atomic design?</b></summary>

Компоненты организованы по сложности: atoms (button, input) → molecules (поле поиска) → organisms (header) → templates → pages. Преимущества: консистентная дизайн-система, понятная иерархия, переиспользуемые примитивы.
</details>

## Настройка окружения

<details>
<summary><b>Какие инструменты и зависимости нужны для настройки локальной среды разработки React-проекта?</b></summary>

Node.js и npm/yarn, редактор кода (VS Code), расширение React DevTools для браузера, Git. Опционально: ESLint, Prettier, TypeScript. Для CRA нужен только Node.js — всё остальное включено.
</details>

<details>
<summary><b>Как вы управляете переменными окружения в React-проекте?</b></summary>

Используйте файлы `.env` (`.env.development`, `.env.production`). Переменные должны начинаться с `REACT_APP_`. Доступ через `process.env.REACT_APP_*`. Никогда не коммитьте секреты — используйте `.env.local` для чувствительных данных.
</details>

<details>
<summary><b>Какие инструменты или техники вы используете для отладки и решения проблем в React-приложении?</b></summary>

React DevTools (инспекция компонентов, state, props), браузерные DevTools (console, network, breakpoints), стратегический console.log, Redux DevTools для state. Error boundaries для отлова ошибок.
</details>

<details>
<summary><b>Какие дополнительные настройки вы обычно выполняете для оптимизации локального рабочего процесса?</b></summary>

ESLint + Prettier для качества кода, husky для pre-commit hooks, path aliases для чистых импортов, расширения VS Code (ES7 snippets), TypeScript для типобезопасности, настройка hot reloading.
</details>

## Роутинг и навигация

<details>
<summary><b>Как реализовать роутинг в React-приложении?</b></summary>

React Router — стандарт. Установите `react-router-dom`. Оберните приложение в `BrowserRouter`. Используйте компоненты `Routes` и `Route`. `Link` для навигации. Поддерживает вложенные роуты, params, query strings.
</details>

<details>
<summary><b>Как обработать сценарий 404 страница не найдена в React Router?</b></summary>

Добавьте catch-all роут в конце: `<Route path="*" element={<NotFound />} />`. Совпадает со всем, что не совпало с предыдущими роутами.
</details>

<details>
<summary><b>Какие есть React Router hooks?</b></summary>

Hooks v6: `useNavigate()` (заменяет useHistory), `useParams()`, `useLocation()`, `useSearchParams()`. Пример:
```javascript
const navigate = useNavigate();
navigate('/dashboard'); // редирект
navigate(-1); // назад
```
</details>

<details>
<summary><b>Как реализовать защищённые роуты?</b></summary>

Создайте компонент ProtectedRoute, который проверяет статус авторизации. Если не авторизован, редирект на login. Пример:
```javascript
const ProtectedRoute = ({ children }) => {
  const isAuth = useAuth();
  return isAuth ? children : <Navigate to="/login" />;
};
```
</details>

## Управление данными

<details>
<summary><b>В чём разница между controlled и uncontrolled компонентами в React?</b></summary>

- **Controlled**: React state управляет значением input. `value` + `onChange` handler. React — источник истины
- **Uncontrolled**: DOM управляет значением. Используйте `ref` для доступа. `defaultValue` для начального значения

Controlled предпочтительнее — более предсказуемы.
</details>

<details>
<summary><b>Как обрабатывать асинхронную загрузку данных в React?</b></summary>

Используйте `useEffect` для fetch при mount. Управляйте состояниями loading/error. Рассмотрите библиотеки: React Query, SWR (кэширование, refetching, dedupe). async/await в useEffect требует cleanup для race conditions.
</details>

<details>
<summary><b>Как управлять shared или глобальным state между разными компонентами?</b></summary>

Варианты: поднятие state вверх, Context API (встроенный, хорош для простых случаев), Redux (сложные приложения), Zustand (простой API), Jotai/Recoil (атомарный). Выбирайте исходя из сложности и знакомства команды.
</details>

<details>
<summary><b>В чём разница между server state и application state?</b></summary>

- **Server state**: Данные, хранящиеся на сервере или во внешних сервисах, обычно получаемые через API. Примеры: профиль пользователя из БД, список продуктов, комментарии. Характеристики: асинхронный, может устареть, нужна стратегия кэширования.

- **Application state**: Данные, специфичные для взаимодействия пользователя с приложением. Примеры: UI state (модалки, табы), пользовательские настройки, поля форм, клиентские фильтры. Характеристики: синхронный, локальный, временный.

**Инструменты для каждого:**
- Server state: React Query, SWR, Apollo Client
- Application state: useState, useReducer, Zustand, Redux
</details>

<details>
<summary><b>Какой рекомендуемый способ получения внешних данных в React?</b></summary>

Используйте **useEffect** hook для получения данных при mount компонента или при изменении зависимостей. Храните полученные данные в state через useState или useReducer.

**Библиотеки:**
- **REST APIs**: axios, fetch, React Query, SWR
- **GraphQL APIs**: Apollo Client, Relay, urql

**Современные подходы:**
- **React Query / SWR**: Встроенные кэширование, refetching, дедупликация
- **tRPC (T3 Stack)**: End-to-end типобезопасные API
- **Server Components (Next.js)**: Получение данных на сервере, не нужен клиентский fetching

```javascript
// Традиционный подход
useEffect(() => {
  fetch('/api/data').then(res => res.json()).then(setData);
}, []);

// Подход React Query
const { data, isLoading } = useQuery(['data'], fetchData);
```
</details>

## SEO

<details>
<summary><b>Что такое SEO и почему это важно для сайта?</b></summary>

Search Engine Optimization — делает сайт обнаруживаемым поисковыми системами. Важно для: органического трафика, видимости, доверия. Включает: хороший контент, мета-теги, производительность, mobile-friendly, семантический HTML.
</details>

<details>
<summary><b>Как обеспечить SEO-дружественность Single-Page Application на React?</b></summary>

Используйте SSR (Next.js) или SSG для предварительно отрендеренного HTML. Добавьте мета-теги (react-helmet). Реализуйте правильный роутинг. Используйте семантический HTML. Создайте sitemap. Обеспечьте быструю загрузку.
</details>

<details>
<summary><b>Что такое SPA?</b></summary>

Single Page Application — загружается один раз, контент обновляется динамически без полной перезагрузки страницы. JavaScript управляет роутингом. Быстрая навигация после начальной загрузки. Примеры: Gmail, Facebook.
</details>

<details>
<summary><b>Какие основные проблемы SPA с SEO?</b></summary>

Поисковые системы могут не выполнять JavaScript. Пустой начальный HTML. Медленное время до контента. Динамические мета-теги не видны. Проблемы с sharing в соцсетях (нет preview).
</details>

<details>
<summary><b>Какие решения?</b></summary>

Server-Side Rendering (SSR), Static Site Generation (SSG), prerendering-сервисы, dynamic rendering для ботов. Next.js/Gatsby решают это. Правильные мета-теги с react-helmet-async.
</details>

<details>
<summary><b>В каких случаях стоит строить SPA?</b></summary>

SPA идеальны для:
- **Mobile app-подобный опыт и PWA**: Плавные переходы, offline-поддержка
- **Сложное управление state**: Постоянный state между views, real-time обновления
- **Высоко интерактивные UI**: Нет перезагрузок страницы, быстрые переходы между views
- **Dashboard-приложения**: Частое взаимодействие пользователя, частые обновления
- **Приложения за аутентификацией**: SEO менее важен

Избегайте SPA для: контентных сайтов, требующих SEO, простых информационных сайтов, блогов.
</details>

<details>
<summary><b>Что такое мета-фреймворк в контексте веб-разработки?</b></summary>

Мета-фреймворк — это фреймворк, построенный поверх других фреймворков или библиотек, предоставляющий дополнительные возможности и соглашения.

**Примеры:**
- **Next.js** → построен на React.js (добавляет SSR, роутинг, API routes)
- **Nuxt.js** → построен на Vue.js
- **Remix** → построен на React (альтернатива Next.js)
- **SvelteKit** → построен на Svelte
- **NestJS** → построен на Express/Fastify (бэкенд)

Мета-фреймворки предоставляют: file-based роутинг, SSR/SSG, API routes, оптимизацию, решения для деплоя.
</details>

<details>
<summary><b>Как задеплоить React-приложение без мета-фреймворка?</b></summary>

Шаги для деплоя чистого React SPA:

1. **Build script**: Добавьте build script в package.json (`npm run build`)
2. **Выберите провайдера**: Выберите хостинг, поддерживающий SPA (Netlify, Vercel, AWS S3 + CloudFront, GitHub Pages)
3. **Деплой**: Через CLI, FTP или git remote repository
4. **Создайте сборку**: Запустите `npm run build` для создания production bundle
5. **Настройте сервер**: Укажите на директорию сборки (обычно `dist` или `build`)
6. **Обработка роутинга**: Настройте редиректы для клиентского роутинга (редирект всех роутов на index.html)

```json
// _redirects файл для Netlify
/*    /index.html   200
```
</details>

## Forms

<details>
<summary><b>Как обрабатывать отправку форм в React?</b></summary>

Добавьте `onSubmit` к элементу form. Вызовите `e.preventDefault()` для предотвращения перезагрузки страницы. Доступ к данным формы из state (controlled) или FormData API. Пример:
```javascript
const handleSubmit = (e) => { e.preventDefault(); // обработка данных };
```
</details>

<details>
<summary><b>Как выполнять валидацию форм в React-приложении?</b></summary>

Варианты: ручная валидация в onChange/onSubmit, валидация схемой Yup, Zod для TypeScript. Библиотеки типа Formik и React Hook Form имеют встроенную интеграцию валидации.
</details>

<details>
<summary><b>Объясните назначение события onChange в React-формах?</b></summary>

`onChange` срабатывает при каждом изменении input. Обновляйте state новым значением: `onChange={(e) => setName(e.target.value)}`. Поддерживает синхронизацию React state с input (controlled component).
</details>

<details>
<summary><b>Знакомы ли вы с библиотеками форм типа Formik или React Hook Form?</b></summary>

- **Formik**: Декларативный, обрабатывает validation/errors/touched, хорош для сложных форм
- **React Hook Form**: Фокус на производительности (меньше re-renders), uncontrolled по умолчанию, меньший bundle

Используйте для: сложной валидации, множества полей, динамических форм.
</details>

<details>
<summary><b>Как сбросить форму или очистить значения input в React?</b></summary>

Controlled: сбросьте state к начальным значениям. Можно использовать `form.reset()` для uncontrolled. React Hook Form имеет метод `reset()`. Formik имеет `resetForm()`.
</details>

<details>
<summary><b>Как обрабатывать загрузку файлов в React-форме?</b></summary>

Используйте `<input type="file">`. Доступ к файлу через `e.target.files[0]`. Отправьте с FormData на backend. Учитывайте: ограничения размера файла, разрешённые типы, индикатор прогресса, preview для изображений.
</details>

## Formik, YUP и React Hook Form

<details>
<summary><b>Какие преимущества Formik?</b></summary>

Уменьшает boilerplate, управляет: values, errors, touched, validation, submission. Лёгкая интеграция с Yup. Компоненты `Field` и `ErrorMessage`. Хорошая документация.
</details>

<details>
<summary><b>Как создать динамическую форму с динамическими полями?</b></summary>

Используйте `FieldArray` от Formik для массивов полей. Можно добавлять/удалять поля динамически. Доступ через `arrayHelpers.push()`, `arrayHelpers.remove(index)`.
</details>

<details>
<summary><b>Как добавить ошибки от backend к форме?</b></summary>

Formik: используйте `setErrors()` или `setFieldError()` после ответа API. React Hook Form: `setError('fieldName', { message: 'error' })`.
</details>

<details>
<summary><b>Как валидировать данные формы?</b></summary>

Formik: функция `validate` или `validationSchema` (Yup). React Hook Form: `resolver` с Yup/Zod или проп `rules` на register.
</details>

<details>
<summary><b>Какие преимущества YUP?</b></summary>

Декларативная валидация схемой. Цепочечные методы. Встроенные валидаторы (email, url, min, max). Простые сообщения об ошибках. Хорошо работает с TypeScript. Схема переиспользуема.
</details>

<details>
<summary><b>Как валидировать динамические поля с YUP?</b></summary>

Используйте `Yup.array().of(schema)` для полей-массивов. Каждый элемент валидируется по внутренней схеме. Можно добавить `min()`, `max()` для длины массива.
</details>

<details>
<summary><b>Какие преимущества React-hook-forms?</b></summary>

Производительность (минимум re-renders), маленький размер bundle, лёгкая интеграция с UI-библиотеками, встроенная валидация, поддержка TypeScript, uncontrolled inputs по умолчанию.
</details>

<details>
<summary><b>Какие преимущества useFormContext?</b></summary>

Доступ к методам формы во вложенных компонентах без prop drilling. Оберните форму в `FormProvider`. Дочерние компоненты используют `useFormContext()` для доступа к register, errors и т.д.
</details>

## Components и Lifecycle

<details>
<summary><b>Какие фазы жизненного цикла компонентов ReactJS?</b></summary>

Три фазы:
- **Mounting**: constructor, render, componentDidMount (useEffect с [])
- **Updating**: render, componentDidUpdate (useEffect с deps)
- **Unmounting**: componentWillUnmount (cleanup в useEffect)
</details>

<details>
<summary><b>Объясните разницу между функциональными и классовыми компонентами.</b></summary>

- **Class**: ES6 класс, `this.state`, lifecycle-методы, более многословно
- **Functional**: Простые функции, hooks для state/effects, проще, предпочтительны сейчас

Функциональные компоненты с hooks — современный стандарт.
</details>

<details>
<summary><b>В чём разница между Element и Component в React?</b></summary>

- **Element**: Простой объект, описывающий что рендерить. Иммутабельный. Создаётся через JSX: `<div>Hello</div>`
- **Component**: Функция или класс, возвращающий elements. Переиспользуемый, может иметь state/props
</details>

<details>
<summary><b>Как очищать ресурсы или выполнять cleanup при использовании React Hooks?</b></summary>

Возвращаемая функция из useEffect выполняется при cleanup:
```javascript
useEffect(() => {
  const subscription = subscribe();
  return () => subscription.unsubscribe(); // cleanup
}, []);
```
Выполняется перед следующим effect и при unmount.
</details>

## Virtual DOM и Reconciliation

<details>
<summary><b>В чём разница между DOM и virtual DOM в React.js?</b></summary>

- **DOM**: Браузерное представление HTML. Медленно обновлять напрямую
- **Virtual DOM**: JavaScript-копия DOM. React сначала обновляет virtual, сравнивает с реальным DOM, обновляет только изменённые части (эффективно)
</details>

<details>
<summary><b>Объясните основы React Reconciliation</b></summary>

Reconciliation — алгоритм сравнения. Сравнивает старый и новый virtual DOM. Правила: разные типы = перестроить, одинаковый тип = обновить атрибуты, keys помогают идентифицировать элементы списка. Минимизирует реальные DOM-операции.
</details>

<details>
<summary><b>В чём разница между ShadowDOM и VirtualDOM?</b></summary>

- **Shadow DOM**: Браузерная фича для инкапсуляции. Скрывает внутреннюю структуру. Используется Web Components
- **Virtual DOM**: JavaScript-абстракция для эффективных обновлений. Концепция React

Разные цели — изоляция vs производительность.
</details>

## Refs

<details>
<summary><b>Refs следует использовать в следующих случаях — объясните</b></summary>

Используйте refs для: доступа к DOM (focus, scroll, измерения), интеграции со сторонними библиотеками, хранения мутабельных значений, не вызывающих re-render, сохранения ссылок на intervals/timeouts.
</details>

<details>
<summary><b>В чём разница между useRef и createRef?</b></summary>

- `useRef`: Hook, сохраняется между renders, возвращает тот же объект
- `createRef`: Создаёт новый ref при каждом вызове, для классовых компонентов

В функциональных компонентах всегда используйте `useRef`.
</details>

## Hooks

<details>
<summary><b>Какие правила хуков существуют?</b></summary>

1. Вызывайте хуки только на верхнем уровне (не внутри циклов, условий, вложенных функций)
2. Вызывайте хуки только из React-функций (компоненты или custom hooks)

Правила существуют потому что React полагается на порядок вызовов для связывания state с хуками.
</details>

<details>
<summary><b>Почему нельзя вызывать хуки условно?</b></summary>

React отслеживает хуки по порядку их вызова при каждом рендере. Если вызывать хуки условно, порядок меняется между рендерами, и React не может сопоставить state с правильным хуком. Всегда вызывайте все хуки, затем используйте условия внутри.
</details>

<details>
<summary><b>Что произойдёт если опустить массив зависимостей в useEffect?</b></summary>

Effect выполняется после каждого рендера. Это может вызвать проблемы с производительностью или бесконечные циклы, если effect обновляет state. Всегда указывайте зависимости, если только намеренно не хотите выполнять на каждом рендере.
</details>

<details>
<summary><b>В чём разница между useEffect и useLayoutEffect?</b></summary>

- `useEffect`: Запускается асинхронно после отрисовки браузером. Неблокирующий. Используйте для большинства side effects
- `useLayoutEffect`: Запускается синхронно после мутаций DOM, до отрисовки. Блокирует визуальные обновления

Используйте `useLayoutEffect` только когда нужно измерить/изменить DOM до того, как пользователь увидит (tooltips, анимации).
</details>

<details>
<summary><b>Когда НЕ стоит использовать useMemo?</b></summary>

Не используйте когда:
- Вычисление дешёвое (простая математика, конкатенация строк)
- Значение меняется при большинстве рендеров
- Преждевременная оптимизация (сначала профилируйте)

useMemo имеет overhead (сравнение, память). Используйте только для дорогих вычислений, которые не часто меняются.
</details>

<details>
<summary><b>Можно ли хранить не-DOM значения в useRef?</b></summary>

Да. useRef может хранить любое мутабельное значение, которое сохраняется между рендерами без вызова re-render. Используйте для: предыдущих значений, timer IDs, instance-переменных, любых значений которые нужно хранить но не в state.
</details>

<details>
<summary><b>Что такое useTransition и useDeferredValue?</b></summary>

Concurrent-фичи React 18 для несрочных обновлений:
- `useTransition`: Помечает обновление state как несрочное, сохраняет UI отзывчивым
- `useDeferredValue`: Откладывает обновление значения, показывает устаревшие данные во время transitions

Используйте для дорогих рендеров (фильтрация больших списков) сохраняя input отзывчивым.
</details>

<details>
<summary><b>Какие преимущества использования React Hooks?</b></summary>

Более простой код, sharing stateful логики (custom hooks), нет сложности классов, лучшая поддержка TypeScript, более простое тестирование, colocation связанной логики, нет путаницы с lifecycle-методами.
</details>

<details>
<summary><b>В чём разница между useMemo и useCallback?</b></summary>

- `useMemo`: Мемоизирует вычисленное значение. Возвращает значение
- `useCallback`: Мемоизирует функцию. Возвращает функцию

`useCallback(fn, deps)` равен `useMemo(() => fn, deps)`.
</details>

<details>
<summary><b>Обновляется ли React useState Hook мгновенно?</b></summary>

Нет, обновления state батчатся и асинхронны. Новое значение доступно на следующем render. Для немедленного использования нового значения используйте функциональное обновление: `setState(prev => prev + 1)`. Или useRef для немедленного доступа.
</details>

<details>
<summary><b>Объясните почему useState hook принимает функцию как начальное значение</b></summary>

Когда вы передаёте функцию в useState, это называется **ленивая инициализация**. Функция выполняется только один раз при начальном рендере, а не при каждом ре-рендере.

```javascript
// Дорогое вычисление выполняется на КАЖДОМ рендере
const [state, setState] = useState(expensiveCalculation());

// Дорогое вычисление выполняется только ОДИН РАЗ при начальном рендере
const [state, setState] = useState(() => expensiveCalculation());
```

Используйте ленивую инициализацию когда:
- Начальное значение требует дорогого вычисления
- Чтение из localStorage/sessionStorage
- Парсинг JSON или обработка данных
</details>

<details>
<summary><b>В чём разница между useState и useReducer?</b></summary>

- **useState**: Лучше для простого управления state без сложной логики. Одно значение или простые объекты.
- **useReducer**: Предназначен для сложной логики state с несколькими подзначениями, переходами состояний и dispatch actions.

```javascript
// useState — простой state
const [count, setCount] = useState(0);

// useReducer — сложный state с actions
const [state, dispatch] = useReducer(reducer, initialState);
dispatch({ type: 'INCREMENT' });
```

Используйте useReducer когда: логика state сложная, следующее состояние зависит от предыдущего, несколько связанных значений меняются вместе, нужны предсказуемые переходы состояний.
</details>

<details>
<summary><b>Как использовать переиспользуемые Hooks?</b></summary>

Извлеките общую логику в custom hooks (префикс `use`). Возвращайте нужные значения/функции. Примеры: `useLocalStorage`, `useFetch`, `useDebounce`. Можно sharing между компонентами или проектами.
</details>

## Производительность и ре-рендеринг

<details>
<summary><b>При каких обстоятельствах компонент ре-рендерится в React?</b></summary>

Компонент ре-рендерится когда:

1. **Изменение state**: Когда state компонента обновляется через setState
2. **Изменение props**: Когда компонент получает новые props (даже если значения одинаковые по ссылке)
3. **Ре-рендер родителя**: Когда родительский компонент ре-рендерится, дети ре-рендерятся по умолчанию
4. **Изменение context**: Когда потребляемое значение context изменяется через useContext
5. **Hooks с зависимостями**: Когда изменяются зависимости useEffect, useMemo, useCallback, эффект выполняется и может вызвать ре-рендер
</details>

<details>
<summary><b>Как предотвратить ненужные ре-рендеры?</b></summary>

1. **React.memo**: Оберните функциональные компоненты для предотвращения ре-рендера если props не изменились
2. **useMemo**: Мемоизируйте дорогие вычисленные значения
3. **useCallback**: Мемоизируйте callback-функции, передаваемые как props
4. **Правильные массивы зависимостей**: Корректно настраивайте зависимости hooks
5. **useRef для значений форм**: Для больших форм предпочитайте useRef вместо useState чтобы избежать ре-рендеров на каждом нажатии клавиши
6. **State colocation**: Держите state как можно ближе к месту использования
</details>

<details>
<summary><b>Какое преимущество использования React.memo API?</b></summary>

React.memo — higher-order component, предотвращающий ненужные ре-рендеры когда props компонента не изменились.

```javascript
const MyComponent = React.memo(function MyComponent({ name, count }) {
  return <div>{name}: {count}</div>;
});
```

**Преимущества:**
- Улучшает производительность пропуском ре-рендеров
- По умолчанию выполняет shallow сравнение props
- Можно предоставить кастомную функцию сравнения как второй аргумент

**Используйте когда:** Компонент рендерится часто с одинаковыми props, рендеры дорогие, компонент чистый (одинаковые props = одинаковый output).
</details>

<details>
<summary><b>Что такое виртуализация? Для чего она нужна?</b></summary>

Виртуализация — техника оптимизации рендеринга больших списков или grid путём рендеринга только видимых элементов на экране.

**Преимущества:**
- Уменьшает количество создаваемых и обновляемых DOM-элементов
- Минимизирует использование памяти
- Уменьшает вычисления layout
- Обеспечивает плавный скролл через тысячи элементов

**Библиотеки:** react-window, react-virtualized, TanStack Virtual

```javascript
import { FixedSizeList } from 'react-window';

<FixedSizeList height={400} itemCount={10000} itemSize={35} width={300}>
  {({ index, style }) => <div style={style}>Строка {index}</div>}
</FixedSizeList>
```

Используйте виртуализацию для списков с 100+ элементами или при проблемах с производительностью скролла.
</details>

## HOC и продвинутые паттерны

<details>
<summary><b>Какие преимущества использования HOC?</b></summary>

Higher-Order Components: функция, принимающая компонент и возвращающая улучшенный компонент. Преимущества: переиспользование логики, cross-cutting concerns (auth, logging). Заменяются custom hooks, но всё ещё полезны.
</details>

<details>
<summary><b>Что такое Prop-drilling в ReactJS?</b></summary>

Передача props через множество уровней компонентов, чтобы достичь глубокого child. Проблемы: многословность, сложность поддержки. Решения: Context API, библиотеки управления состоянием, композиция компонентов.
</details>

<details>
<summary><b>Что такое Lazy Loading в ReactJS?</b></summary>

Загрузка компонентов только при необходимости. Используйте `React.lazy()` + `Suspense`. Уменьшает начальный размер bundle. Хорошо для роутов, модальных окон, тяжёлых компонентов.
```javascript
const LazyComponent = React.lazy(() => import('./Component'));
```
</details>

## Управление состоянием

<details>
<summary><b>Как Context вызывает проблемы с производительностью?</b></summary>

Каждый компонент, потребляющий контекст, ре-рендерится при изменении значения контекста, даже если использует только часть. Решения: разбить на несколько контекстов, мемоизировать значение provider, использовать селекторы состояния (Zustand), или рассмотреть другие state managers для частых обновлений.
</details>

<details>
<summary><b>Как предотвратить лишние ре-рендеры от Context?</b></summary>

1. Разделите контекст по областям (UserContext, ThemeContext)
2. Мемоизируйте значение контекста: `useMemo(() => ({ user }), [user])`
3. Используйте React.memo на потребляющих компонентах
4. Рассмотрите state на селекторах (Zustand, Jotai) для гранулярных обновлений
</details>

<details>
<summary><b>Какие альтернативы Redux в 2025?</b></summary>

- **Zustand**: Простой, минимальный boilerplate, на селекторах
- **Jotai**: Атомарная модель состояния, подход снизу-вверх
- **Valtio**: На proxy, мутабельный стиль API
- **React Query/TanStack Query**: Для серверного состояния
- **Recoil**: Атомарное состояние от Facebook (менее активен)

Выбирайте исходя из: сложности приложения, предпочтений команды, размера bundle.
</details>

<details>
<summary><b>Как Redux Toolkit улучшает Redux?</b></summary>

- `createSlice`: Объединяет reducer + actions, использует Immer для иммутабельных обновлений
- `configureStore`: Включает Redux DevTools и middleware по умолчанию
- `createAsyncThunk`: Упрощённые async actions
- RTK Query: Встроенный data fetching/caching

Меньше boilerplate, лучшие дефолты, те же концепции Redux.
</details>

<details>
<summary><b>Что такое optimistic UI обновление?</b></summary>

Обновление UI немедленно, предполагая успех, откат при ошибке. Лучший UX — ощущение мгновенности. Реализация: обновить state, отправить запрос, откатить при ошибке:
```javascript
const prev = state;
setState(optimisticValue);
try { await api.update(); } catch { setState(prev); }
```
</details>

## Events

<details>
<summary><b>Опишите как события обрабатываются в React.</b></summary>

React использует обёртку SyntheticEvent. camelCase именование. Event handlers как props. Event pooling (переиспользование). Доступ к нативному событию через `e.nativeEvent`. stopPropagation и preventDefault работают нормально.
</details>

<details>
<summary><b>Что такое Synthetic event?</b></summary>

Кроссбраузерная обёртка React над нативными событиями. Одинаковый интерфейс во всех браузерах. Автоматически очищается. Доступ через параметр event в handler. Содержит: target, currentTarget, type и т.д.
</details>

## Next.js и SSR

<details>
<summary><b>Какие преимущества Next.js?</b></summary>

Преимущества: SSR/SSG из коробки, file-based роутинг, API routes, оптимизация изображений, автоматический code splitting, поддержка TypeScript, отличный developer experience. Хорош для SEO-критичных приложений.
</details>

<details>
<summary><b>Что такое SSR?</b></summary>

Server-Side Rendering — HTML генерируется на сервере для каждого запроса. Пользователь сразу видит контент. Лучше для SEO, быстрее воспринимаемая загрузка. Trade-off: нагрузка на сервер, TTFB может быть медленнее.
</details>

<details>
<summary><b>Какие типы pre-rendering доступны в Next JS?</b></summary>

Два типа:
- **SSG** (Static Site Generation): HTML генерируется во время сборки
- **SSR** (Server-Side Rendering): HTML генерируется при каждом запросе

Также ISR (Incremental Static Regeneration) — пересборка страниц в фоне.
</details>

<details>
<summary><b>Различия между типами pre-rendering в Next JS?</b></summary>

- **SSG**: Лучшая производительность, используйте для статического контента. `getStaticProps`
- **SSR**: Всегда свежие данные, используйте для динамического контента. `getServerSideProps`
- **ISR**: Лучшее из обоих — статика с ревалидацией. Опция `revalidate`
</details>

<details>
<summary><b>Какие свойства доступны в объекте context при использовании serverSideProps?</b></summary>

Context содержит: `params` (параметры роута), `req` (объект запроса), `res` (объект ответа), `query` (query string), `preview` (статус preview mode), `resolvedUrl`.
</details>

<details>
<summary><b>Объясните важность code splitting в Next JS и dynamic import?</b></summary>

Code splitting уменьшает размер bundle. Каждая страница — отдельный chunk. Dynamic imports (`next/dynamic`) для компонентов, загружаемых по требованию. Улучшает время начальной загрузки.
</details>

<details>
<summary><b>Какова цель функции getStaticPaths?</b></summary>

`getStaticPaths` используется когда динамическая страница использует `getStaticProps`. Next.js нужно знать все возможные пути для динамического роута во время сборки.

```javascript
// pages/posts/[id].js
export async function getStaticPaths() {
  const posts = await fetchPosts();
  return {
    paths: posts.map(post => ({ params: { id: post.id } })),
    fallback: false // или 'blocking' или true
  };
}
```

**Варианты fallback:**
- `false`: 404 для неизвестных путей
- `true`: Генерация страницы по требованию, показ состояния загрузки
- `'blocking'`: Генерация по требованию, SSR-подобное поведение

Можно использовать `getStaticProps` без `getStaticPaths` для нединамических роутов.
</details>

<details>
<summary><b>Как работает next/image API? Почему он улучшает производительность?</b></summary>

Компонент `next/image` автоматически оптимизирует изображения:

1. **Серверная оптимизация**: Изображения изменяют размер, конвертируются в формат (WebP), сжимаются
2. **Lazy loading**: Изображения загружаются только при входе во viewport
3. **Адаптивные размеры**: Отдаёт подходящий размер для устройства
4. **Кэширование**: Оптимизированные изображения кэшируются с заголовками для браузера/CDN

```javascript
import Image from 'next/image';

<Image
  src="/photo.jpg"
  width={500}
  height={300}
  alt="Описание"
  priority // для изображений above-the-fold
/>
```

**Преимущества для производительности:** Меньший размер файлов, быстрая загрузка страниц, лучшие Core Web Vitals (LCP), предотвращение сдвигов макета (CLS).
</details>

<details>
<summary><b>Как задеплоить Next.js приложение не на Vercel?</b></summary>

Next.js можно задеплоить на любую платформу, поддерживающую Node.js:

1. **Build**: `npm run build`
2. **Start**: `npm run start` (требует Node.js сервер)
3. **Платформы**: AWS EC2/ECS, DigitalOcean, Railway, Render, Docker containers, любой VPS

**Для статического экспорта** (без SSR):
```javascript
// next.config.js
module.exports = { output: 'export' }
```
Затем деплой на любой статический хостинг (S3, Netlify, GitHub Pages).

Единственное отличие от Vercel — вы управляете инфраструктурой сами, а не получаете автоматизацию.
</details>

<details>
<summary><b>Как работают API routes в Next.js?</b></summary>

Next.js API routes предоставляют встроенные бэкенд-endpoints внутри Next.js приложения. Создайте файлы внутри `pages/api/` (или `app/api/` в App Router) — они становятся серверными функциями.

```javascript
// pages/api/users.js
export default function handler(req, res) {
  if (req.method === 'GET') {
    res.status(200).json({ users: [] });
  } else if (req.method === 'POST') {
    // Создание пользователя
    res.status(201).json({ success: true });
  }
}
```

**Возможности:** Доступ к объектам request/response, поддержка middleware, можно подключаться к базам данных, готовность к serverless деплою.
</details>

<details>
<summary><b>Можно ли использовать API Routes если приложение не на Vercel?</b></summary>

Да, Next.js API routes работают на любой платформе, поддерживающей Node.js. Они не специфичны для Vercel.

**Требования:**
- Работающий Node.js сервер (не статический экспорт)
- `npm run build` + `npm run start`

Работает на: AWS, DigitalOcean, Heroku, Railway, любом VPS с Node.js. Runtime одинаковый независимо от хостинг-провайдера.
</details>

<details>
<summary><b>Какое преимущество использования Serverless режима?</b></summary>

Serverless деплой для Next.js предлагает:

- **Улучшенная масштабируемость**: Функции автоматически масштабируются по нагрузке
- **Экономичность**: Платите только за фактически используемые compute-ресурсы
- **Проще деплой**: Нет управления серверами или инфраструктурой
- **Быстрее время отклика**: Функции деплоятся ближе к пользователям (edge locations)
- **Нет cold starts** (на Vercel): Оптимизировано для Next.js

Лучше всего для: переменного трафика, проектов с ограниченным бюджетом, потребностей в глобальном распространении.
</details>

<details>
<summary><b>Можно ли использовать статический CDN с Next.js?</b></summary>

Да, настройте опцию `assetPrefix` в `next.config.js`:

```javascript
// next.config.js
module.exports = {
  assetPrefix: 'https://cdn.example.com',
}
```

Это добавляет префикс ко всем статическим ассетам (JS, CSS, изображения) с URL вашего CDN. CDN отдаёт статические файлы, а Next.js сервер обрабатывает SSR-страницы.

Для полностью статических сайтов используйте `output: 'export'` и деплойте всю сборку на CDN.
</details>

<details>
<summary><b>Как интегрировать AMP с Next.js?</b></summary>

Импортируйте `withAmp` higher-order component и оберните страницу:

```javascript
import { withAmp } from 'next/amp';

function MyPage() {
  return <div>AMP-контент страницы</div>;
}

export default withAmp(MyPage);
// или для гибридного: export default withAmp(MyPage, { hybrid: true });
```

**Режимы:**
- **AMP-only**: Страница отдаётся только как AMP
- **Hybrid**: Доступны обе версии — AMP и обычная

Примечание: Поддержка AMP сейчас используется реже, так как Core Web Vitals можно достичь без AMP.
</details>

## I18n (Интернационализация)

<details>
<summary><b>Как реализовать локализацию в React?</b></summary>

Библиотеки: react-i18next, react-intl. Настройка: конфигурация языков, создание файлов переводов (JSON), обёртка приложения provider, использование translation hook/component.
</details>

<details>
<summary><b>Как использовать динамические строки в сообщениях локализации в React?</b></summary>

Используйте интерполяцию. i18next: `t('greeting', { name: 'John' })` с `"greeting": "Hello {{name}}"`. react-intl: `<FormattedMessage values={{ name }}/>`.
</details>

<details>
<summary><b>Как делать lazy loading переводов в React?</b></summary>

Загрузка переводов по требованию по языку/namespace. i18next имеет backend plugins для async загрузки. Загружайте при переключении языка пользователем или входе на роут.
</details>

<details>
<summary><b>Есть ли у вас опыт и как это было реализовано?</b></summary>

(Личный вопрос — опишите ваш проект, встреченные сложности, используемую библиотеку, структуру папок для переводов, обработку plural и дат.)
</details>

## PWA и Service Workers

<details>
<summary><b>Что такое progressive web app?</b></summary>

Веб-приложение с native-подобными фичами: устанавливаемое, работает offline, push-уведомления, быстрая загрузка. Использует: service workers, manifest file, HTTPS. Связывает веб и нативные приложения.
</details>

<details>
<summary><b>Что такое service worker?</b></summary>

JavaScript, работающий в фоне, отдельно от основного потока. Перехватывает сетевые запросы. Обеспечивает: offline-поддержку, кэширование, push-уведомления, background sync. Lifecycle: install → activate → fetch.
</details>

<details>
<summary><b>Что такое App Shell?</b></summary>

Минимальный HTML/CSS/JS для базовой структуры UI. Кэшируется service worker. Загружается мгновенно. Контент заполняется динамически. Улучшает воспринимаемую производительность.
</details>

<details>
<summary><b>Что такое Web App manifest?</b></summary>

JSON-файл (`manifest.json`), описывающий приложение. Содержит: name, icons, theme color, start URL, display mode. Браузер использует его для prompt установки и иконки на домашнем экране.
</details>

<details>
<summary><b>Какие требования для установки сайта как PWA?</b></summary>

Требования: HTTPS, валидный manifest file, service worker с fetch handler, иконка (512x512), соответствие engagement heuristic (взаимодействие пользователя). Chrome показывает prompt установки.
</details>

## Google API

<details>
<summary><b>Какие сервисы Google API вы использовали?</b></summary>

(Личный вопрос — распространённые: Maps API, Places API, Analytics, OAuth/Sign-in, Firebase, Cloud Storage, Sheets API, YouTube API.)
</details>

## React Style Guide

<details>
<summary><b>Как отделять state и бизнес-логику от UI?</b></summary>

Custom hooks для логики, компоненты для UI. Паттерн Container/presentational. Service layer для API-вызовов. Компоненты получают данные через props, не знают откуда они.
</details>

<details>
<summary><b>Когда следует избегать использования State?</b></summary>

Избегайте state для: производных данных (вычисляйте из существующего state), констант, значений, не используемых в render, данных, которые должны приходить из props. Держите state минимальным.
</details>

<details>
<summary><b>Как использовать Object Destructuring для Props?</b></summary>

Деструктуризация в параметрах функции или в теле:
```javascript
const Component = ({ name, age }) => <div>{name}, {age}</div>;
// или
const Component = (props) => { const { name, age } = props; };
```
</details>

## Парадигмы программирования

<details>
<summary><b>Различия между императивным и декларативным программированием. Какое используется в React?</b></summary>

- **Императивное**: Пошаговое как что-то делать (for loops, DOM manipulation)
- **Декларативное**: Описываете что вы хотите (SQL, React JSX)

React декларативный — вы описываете UI на основе state, React обрабатывает DOM-обновления.
</details>

## React под капотом

<details>
<summary><b>Как работает React под капотом?</b></summary>

JSX компилируется в вызовы `React.createElement()`. Создаёт virtual DOM tree. При изменении state: создаёт новое virtual tree, сравнивает со старым (reconciliation), генерирует минимальные DOM-обновления. Fiber-архитектура обеспечивает: async rendering, приоритизацию, отмену обновлений.
</details>

## Server Components и Suspense

<details>
<summary><b>Что такое Server Components?</b></summary>

Компоненты, которые рендерятся на сервере и никогда не отправляются клиенту. Преимущества: нулевой bundle size, прямой доступ к базе/файлам, автоматический code splitting. Используйте для data fetching, тяжёлых зависимостей. Помечайте клиентские компоненты директивой 'use client'.
</details>

<details>
<summary><b>Чем Server Components отличаются от SSR?</b></summary>

- **SSR**: Рендерит полную страницу на сервере, затем гидратирует всё приложение на клиенте. Весь код отправляется клиенту
- **Server Components**: Некоторые компоненты ТОЛЬКО выполняются на сервере, никогда не гидратируются. Уменьшенный JS bundle, можно использовать server-only API

Server Components — часть RSC архитектуры, дополняют SSR.
</details>

<details>
<summary><b>Что такое Suspense boundaries?</b></summary>

Suspense оборачивает компоненты, которые могут "приостановиться" (lazy loading, data fetching). Показывает fallback пока ждёт:
```jsx
<Suspense fallback={<Loading />}>
  <LazyComponent />
</Suspense>
```
Включает streaming SSR, concurrent features. Можно вкладывать для гранулярных loading states.
</details>

<details>
<summary><b>Как работают Error Boundaries?</b></summary>

Классовые компоненты, которые ловят JS ошибки в дочернем дереве. Используйте `componentDidCatch` и `getDerivedStateFromError`. Показывают fallback UI вместо краша приложения. Не ловят: event handlers, async код, SSR, ошибки в самом boundary.
</details>

<details>
<summary><b>Могут ли Error Boundaries ловить async ошибки?</b></summary>

Напрямую нет. Ошибки в промисах, setTimeout, event handlers не ловятся. Решения: оборачивать async вызовы в try/catch и устанавливать error state, использовать error boundary с Suspense для ошибок data fetching в React 18+.
</details>

## Фичи React 19

<details>
<summary><b>Какие новые фичи в React 19?</b></summary>

React 19 улучшает async-обработку:
- **Actions**: Упрощённое управление async state с `useActionState`
- **`use` hook**: Чтение ресурсов (promises, context) в render
- **Обработка форм**: `useFormStatus` для pending states
- **Server Components**: Улучшенная поддержка RSC
- **Document metadata**: Нативная поддержка `<title>`, `<meta>`
- **Загрузка ассетов**: Preloading API для ресурсов

Цель — более простой и чистый async-код.
</details>

## Rendering Strategies

<details>
<summary><b>Что такое CSR, SSR, SSG и ISR в Next.js? Когда использовать каждый?</b></summary>

**CSR (Client-Side Rendering)**
Страница рендерится в браузере. JavaScript загружает данные после загрузки страницы.

```jsx
'use client';

function Page() {
  const [data, setData] = useState(null);

  useEffect(() => {
    fetch('/api/data').then(res => res.json()).then(setData);
  }, []);

  return <div>{data?.title}</div>;
}
```
Когда использовать: дашборды, контент для конкретного пользователя, SEO не важен.

---

**SSR (Server-Side Rendering)**
Страница рендерится на сервере при каждом запросе. Свежие данные каждый раз.

```jsx
// App Router - async компонент с no-store
async function Page() {
  const data = await fetch('https://api.example.com/data', {
    cache: 'no-store'
  });

  return <div>{data.title}</div>;
}
```
Когда использовать: SEO важен, данные часто меняются, нужен свежий контент.

---

**SSG (Static Site Generation)**
Страница рендерится во время сборки. Одинаковый HTML для всех пользователей.

```jsx
// App Router - кэширование по умолчанию
async function Page() {
  const data = await fetch('https://api.example.com/data');
  // По умолчанию результаты fetch кэшируются (поведение SSG)

  return <div>{data.title}</div>;
}
```
Когда использовать: блоги, документация, маркетинговые страницы, контент редко меняется.

---

**ISR (Incremental Static Regeneration)**
Статическая страница, которая перестраивается в фоне через заданное время.

```jsx
async function Page() {
  const data = await fetch('https://api.example.com/data', {
    next: { revalidate: 60 } // Перестроить каждые 60 секунд
  });

  return <div>{data.title}</div>;
}
```
Когда использовать: e-commerce товары, новостные сайты, нужна скорость статики но свежее данные.

---

**Сравнение:**
| Метод | Когда рендерится | Свежесть данных | Производительность |
|-------|-----------------|-----------------|-------------------|
| CSR | Браузер | Real-time | Быстрая загрузка, медленный контент |
| SSR | Каждый запрос | Свежие | Медленнее, хороший SEO |
| SSG | Время сборки | Устаревшие | Самый быстрый |
| ISR | Сборка + интервал | Полу-свежие | Быстрый + обновляемый |

</details>

## Code Splitting

<details>
<summary><b>Что такое Code Splitting?</b></summary>

Code splitting загружает только нужный код. Улучшает производительность и время загрузки. Используйте `React.lazy()` + `Suspense` для компонентов, динамический `import()` для модулей. Часто применяется для route-based splitting.
</details>

## React Patterns

<details>
<summary><b>Что такое Container-Presenter Pattern?</b></summary>

Логика отделена от UI. Container управляет данными/state, Presenter управляет рендерингом. Преимущества: минимум re-renders, максимум контроля, проще тестирование. Container передаёт данные как props в Presenter.
</details>

<details>
<summary><b>Что такое Compound Components?</b></summary>

Паттерн, где родительский компонент управляет поведением детей. Как Radix UI или Headless UI. Дети общаются через shared context. Пример: `<Select><Select.Trigger/><Select.Options/></Select>`. Гибкий API, инкапсулированный state.
</details>

<details>
<summary><b>Что такое Render Props (и их современный эквивалент)?</b></summary>

Старое: передача функции как prop, возвращающей UI. Современное: извлечение логики в custom hooks (`useXXX()`). Та же идея — sharing поведения без sharing реализации. Hooks чище и более компонуемы.
</details>

<details>
<summary><b>Что такое State Colocation Pattern?</b></summary>

Держите state как можно ближе к месту использования. Не поднимайте state выше необходимого. Преимущества: меньше re-renders, проще понять, лучше производительность. Поднимайте только когда действительно нужно для sharing.
</details>

<details>
<summary><b>Что такое Event Propagation Pattern?</b></summary>

Передача callback events между глубоко вложенными компонентами вместо использования context. Лучше для: производительности (нет context re-renders), явного data flow, отладки. Используйте для component-specific events.
</details>

<details>
<summary><b>Что такое Context Module Pattern?</b></summary>

Делайте context модульным, чтобы избежать избыточных re-renders. Разделяйте context по concern, используйте selectors, мемоизируйте context values. Перерендеривайте только компоненты, реально использующие изменённые данные.
</details>

<details>
<summary><b>Что такое Smart Memoization Pattern?</b></summary>

Не мемоизируйте всё — только "нестабильные" части дерева. Используйте `React.memo`, `useMemo`, `useCallback` стратегически. Сначала профилируйте, чтобы найти реальные узкие места. Over-memoization добавляет сложность без пользы.
</details>

<details>
<summary><b>Что такое Layout Shift Prevention Pattern?</b></summary>

Стройте UI так, чтобы избежать скачков при hydration/загрузке. Резервируйте место для async-контента, используйте skeleton loaders, задавайте явные размеры. Предотвращает проблемы CLS (Cumulative Layout Shift).
</details>

<details>
<summary><b>Что такое Suspense + Resource Pattern?</b></summary>

Кэшированные async-ресурсы с React Suspense (React 18+). Создайте resource, который suspends при загрузке. Компонент читает resource, suspends если не готов. Основа современных data layers типа React Query.
</details>

<details>
<summary><b>Что такое Error Boundary Pattern?</b></summary>

Отлов ошибок на уровне UI без краха всего приложения. Class component с `componentDidCatch` и `getDerivedStateFromError`. Показывает fallback UI при ошибке. Используйте на границах route/feature.
</details>

<details>
<summary><b>Что такое State Machine Pattern?</b></summary>

Моделирование сложных UI states явно через state machines (XState или аналоги). Идеально для: форм, checkout flows, платежей, wizards. States и transitions явные, невозможные состояния невозможны.
</details>

<details>
<summary><b>Что такое Stale-While-Revalidate (SWR) Pattern?</b></summary>

Показываем кэшированные данные немедленно, получаем свежие данные в фоне. Используется в Next.js App Router, библиотеке SWR, React Query. Пользователь видит контент мгновенно, получает обновления без блокировки UI.
</details>

<details>
<summary><b>Что такое Adapter Pattern для интеграций?</b></summary>

Единый интерфейс для разных backends/SDK/сторонних данных. Меняйте реализации без изменения компонентов. Пример: один `useAuth()` hook работает с Firebase, Auth0 или кастомной auth.
</details>

<details>
<summary><b>Что такое Selector Pattern в Zustand/Jotai/Recoil?</b></summary>

Разделение state на маленькие selectors, компоненты подписываются только на то, что нужно. Минимум re-renders — компонент обновляется только при изменении его конкретного slice. Пример: `useStore(state => state.user.name)`.
</details>

<details>
<summary><b>Что такое View Transition Pattern?</b></summary>

Плавные анимации между страницами через View Transitions API (2024+). Браузер управляет cross-document transitions. Обеспечивает native-подобные анимации страниц без JS animation libraries.
</details>

<details>
<summary><b>Что такое Islands / Partial Hydration Pattern?</b></summary>

Hydrate только интерактивные части ("islands") страницы. Остальное остаётся статическим HTML. Меньше JS на клиенте, быстрее TTI. Используется в Astro, Qwik. Тренд на 2025 — отправляем меньше JavaScript.
</details>

<details>
<summary><b>Что такое Server Actions + Client Boundaries Pattern?</b></summary>

Новый архитектурный паттерн Next.js. Server Actions обрабатывают мутации без API routes. Чёткие границы между server и client компонентами. Проще data flow, меньше boilerplate.
</details>

## Продвинутая архитектура

<details>
<summary><b>Как бы вы построили архитектуру компонентной библиотеки для масштабируемых UI-систем?</b></summary>

**Ключевые принципы:**

1. **Многоуровневая структура:**
   - Примитивы (atoms): Button, Input, Text
   - Композиты (molecules): SearchField, FormGroup
   - Фичи (organisms): DataTable, Modal

2. **Design tokens:**
```javascript
// tokens.js
export const tokens = {
  colors: { primary: '#007bff', error: '#dc3545' },
  spacing: { sm: '8px', md: '16px', lg: '24px' },
  typography: { body: '16px', heading: '24px' }
};
```

3. **Compound components для гибкости:**
```javascript
<Card>
  <Card.Header>Заголовок</Card.Header>
  <Card.Body>Контент</Card.Body>
  <Card.Footer>Действия</Card.Footer>
</Card>
```

4. **Полиморфный проп `as`:**
```javascript
<Button as="a" href="/link">Кнопка-ссылка</Button>
```

5. **Консистентные паттерны API:**
   - Поддержка controlled/uncontrolled
   - Forwarded refs
   - Spread props на корневой элемент
   - Консистентное именование (onX для событий, isX для boolean)

6. **Документация со Storybook + автоматизированное тестирование**
</details>

<details>
<summary><b>Объясните алгоритм reconciliation и diffing подробно</b></summary>

**Reconciliation в React** сравнивает старое и новое virtual DOM деревья для минимизации реальных DOM-обновлений.

**Ключевые эвристики:**

1. **Разные типы элементов = полная пересборка:**
```jsx
// Старое: <div><Counter /></div>
// Новое: <span><Counter /></span>
// Counter полностью уничтожается и пересоздаётся
```

2. **Одинаковый тип элемента = обновление только атрибутов:**
```jsx
// Старое: <div className="old" />
// Новое: <div className="new" />
// Обновляется только атрибут className
```

3. **Keys для идентификации в списках:**
```jsx
// Без keys: React сопоставляет по индексу (проблемы при reorder)
// С keys: React сопоставляет элементы по key (сохраняет state корректно)
{items.map(item => <Item key={item.id} {...item} />)}
```

**Fiber архитектура (React 16+):**
- Работа разбита на единицы (fibers)
- Рендеринг можно приостановить, возобновить или отменить
- Приоритеты обновлений (взаимодействие пользователя > загрузка данных)
- Concurrent-фичи: Suspense, transitions

**Влияние на производительность:**
- Избегайте без необходимости менять типы элементов
- Используйте стабильные keys (не индекс массива для динамических списков)
- Поднимайте state вверх когда siblings делят state
- Используйте React.memo для дорогих чистых компонентов
</details>

<details>
<summary><b>Оптимизация рендеринга больших списков — подходы кроме виртуализации</b></summary>

1. **Пагинация / Бесконечный скролл:**
```javascript
const [page, setPage] = useState(1);
const items = allItems.slice(0, page * PAGE_SIZE);
```

2. **Debounced рендеринг:**
```javascript
// Рендерим пачками через setTimeout
function renderInBatches(items, batchSize = 50) {
  const [rendered, setRendered] = useState([]);
  useEffect(() => {
    let i = 0;
    function renderBatch() {
      setRendered(items.slice(0, i += batchSize));
      if (i < items.length) setTimeout(renderBatch, 0);
    }
    renderBatch();
  }, [items]);
  return rendered;
}
```

3. **Мемоизация на уровне элемента:**
```javascript
const MemoizedItem = React.memo(Item, (prev, next) =>
  prev.id === next.id && prev.updatedAt === next.updatedAt
);
```

4. **Отложенный рендеринг с `useDeferredValue`:**
```javascript
const deferredList = useDeferredValue(list);
// Показывает устаревшие данные во время обновлений, предотвращая блокировку
```

5. **Web Workers для тяжёлой обработки:**
```javascript
// Обрабатываем/фильтруем данные вне главного потока
const worker = new Worker('list-worker.js');
worker.postMessage({ items, filter });
worker.onmessage = (e) => setProcessedItems(e.data);
```

6. **CSS containment:**
```css
.list-item { contain: layout style paint; }
```
</details>

<details>
<summary><b>Спроектируйте кастомный hook для API polling с backoff</b></summary>

```javascript
function usePolling(fetchFn, {
  interval = 5000,
  maxInterval = 60000,
  backoffMultiplier = 2,
  enabled = true
} = {}) {
  const [data, setData] = useState(null);
  const [error, setError] = useState(null);
  const [isPolling, setIsPolling] = useState(enabled);
  const currentInterval = useRef(interval);
  const timeoutRef = useRef();

  const poll = useCallback(async () => {
    try {
      const result = await fetchFn();
      setData(result);
      setError(null);
      // Сбрасываем интервал при успехе
      currentInterval.current = interval;
    } catch (err) {
      setError(err);
      // Увеличиваем интервал при ошибке (exponential backoff)
      currentInterval.current = Math.min(
        currentInterval.current * backoffMultiplier,
        maxInterval
      );
    }

    if (isPolling) {
      timeoutRef.current = setTimeout(poll, currentInterval.current);
    }
  }, [fetchFn, interval, maxInterval, backoffMultiplier, isPolling]);

  useEffect(() => {
    if (isPolling) {
      poll();
    }
    return () => clearTimeout(timeoutRef.current);
  }, [poll, isPolling]);

  const start = () => setIsPolling(true);
  const stop = () => {
    setIsPolling(false);
    clearTimeout(timeoutRef.current);
  };

  return { data, error, isPolling, start, stop };
}

// Использование
const { data, error, stop } = usePolling(
  () => fetch('/api/status').then(r => r.json()),
  { interval: 3000 }
);
```
</details>

<details>
<summary><b>Как решить проблему stale closures в async React-коде?</b></summary>

**Проблема:** Closures захватывают значения переменных в момент создания, что приводит к устаревшим данным в async-callbacks.

```javascript
// Проблема
function Counter() {
  const [count, setCount] = useState(0);

  const handleClick = () => {
    setTimeout(() => {
      console.log(count); // Всегда логирует начальное значение!
    }, 3000);
  };
}
```

**Решения:**

1. **Используйте refs для текущих значений:**
```javascript
const countRef = useRef(count);
useEffect(() => { countRef.current = count; }, [count]);

const handleClick = () => {
  setTimeout(() => {
    console.log(countRef.current); // Всегда актуальное
  }, 3000);
};
```

2. **Функциональные обновления для setState:**
```javascript
const handleClick = () => {
  setTimeout(() => {
    setCount(prevCount => prevCount + 1); // Использует последнее значение
  }, 3000);
};
```

3. **useCallback с правильными зависимостями:**
```javascript
const handleClick = useCallback(() => {
  // count свежий здесь благодаря зависимости
  console.log(count);
}, [count]);
```

4. **Используйте useEvent (React 18+) или кастомный hook:**
```javascript
function useEvent(handler) {
  const handlerRef = useRef(handler);
  useLayoutEffect(() => { handlerRef.current = handler; });
  return useCallback((...args) => handlerRef.current(...args), []);
}
```
</details>

<details>
<summary><b>Как изолировать обновления глобального state от ре-рендеринга глубоких child-компонентов?</b></summary>

1. **Selector pattern (Zustand/Redux):**
```javascript
// Ре-рендерится только когда меняется user.name
const userName = useStore(state => state.user.name);
```

2. **Разделяйте context по concern:**
```javascript
// Плохо: один context для всего
const AppContext = createContext({ user, theme, settings });

// Хорошо: отдельные contexts
const UserContext = createContext(null);
const ThemeContext = createContext(null);
```

3. **Мемоизируйте context values:**
```javascript
const value = useMemo(() => ({ user, updateUser }), [user]);
return <UserContext.Provider value={value}>{children}</UserContext.Provider>;
```

4. **Композиция компонентов (извлечение children):**
```javascript
// Вместо этого (ре-рендерит children при изменении state):
function Parent() {
  const [state, setState] = useState();
  return <div><ExpensiveChild /></div>;
}

// Делайте так (children не ре-рендерятся):
function Parent({ children }) {
  const [state, setState] = useState();
  return <div>{children}</div>;
}
<Parent><ExpensiveChild /></Parent>
```

5. **React.memo с кастомным сравнением:**
```javascript
const DeepChild = React.memo(Component, (prev, next) => {
  return prev.relevantProp === next.relevantProp;
});
```
</details>

## Задачи с кодом

<details>
<summary><b>Создайте Grid Light Box с LIFO-деактивацией</b></summary>

Создайте сетку кликабельных огней, где клик по огню активирует его, а клик по другому огню деактивирует ранее активированные огни в обратном порядке (LIFO — Last In First Out).

**Требования:**
- Сетка N x M ячеек
- Клик активирует огонь
- Клик по уже активному огню деактивирует его
- Огни деактивируются в обратном порядке активации

```javascript
function GridLightBox({ rows = 3, cols = 3 }) {
  const [activeLights, setActiveLights] = useState([]);

  const handleLightClick = useCallback((id) => {
    setActiveLights(prev => {
      if (prev.includes(id)) {
        // Удаляем если уже активен
        return prev.filter(light => light !== id);
      }
      // Добавляем в стек активации
      return [...prev, id];
    });
  }, []);

  const deactivateLast = useCallback(() => {
    setActiveLights(prev => prev.slice(0, -1));
  }, []);

  const lights = useMemo(() => {
    const result = [];
    for (let i = 0; i < rows * cols; i++) {
      result.push(i);
    }
    return result;
  }, [rows, cols]);

  return (
    <div>
      <div
        style={{
          display: 'grid',
          gridTemplateColumns: `repeat(${cols}, 50px)`,
          gap: '5px'
        }}
      >
        {lights.map(id => (
          <button
            key={id}
            onClick={() => handleLightClick(id)}
            style={{
              width: 50,
              height: 50,
              backgroundColor: activeLights.includes(id) ? 'yellow' : 'gray',
              border: 'none',
              cursor: 'pointer'
            }}
          />
        ))}
      </div>
      <button onClick={deactivateLast} disabled={activeLights.length === 0}>
        Деактивировать последний
      </button>
    </div>
  );
}
```

**Что проверяется:**
- Управление state с массивами (отслеживание порядка активации)
- Корректное использование hooks (useCallback, useMemo)
- Реализация стека LIFO
- Обработка edge cases (клик по тому же огню дважды)
- Соображения производительности (избегание лишних re-renders)

**Дополнительные вопросы:**
- Как добавить анимацию последовательности активации?
- Как добавить функцию "деактивировать все" с задержкой анимации?
- Как сохранить состояние в localStorage?
</details>

<details>
<summary><b>Создайте переиспользуемый компонент таблицы с сортировкой, пагинацией, фильтром и виртуальным скроллом</b></summary>

```javascript
function useTable({ data, columns, pageSize = 10 }) {
  const [sortConfig, setSortConfig] = useState({ key: null, direction: 'asc' });
  const [filter, setFilter] = useState('');
  const [page, setPage] = useState(0);

  // Фильтрация
  const filtered = useMemo(() => {
    if (!filter) return data;
    return data.filter(row =>
      columns.some(col =>
        String(row[col.key]).toLowerCase().includes(filter.toLowerCase())
      )
    );
  }, [data, filter, columns]);

  // Сортировка
  const sorted = useMemo(() => {
    if (!sortConfig.key) return filtered;
    return [...filtered].sort((a, b) => {
      const aVal = a[sortConfig.key];
      const bVal = b[sortConfig.key];
      const direction = sortConfig.direction === 'asc' ? 1 : -1;
      return aVal < bVal ? -direction : aVal > bVal ? direction : 0;
    });
  }, [filtered, sortConfig]);

  // Пагинация
  const paginated = useMemo(() => {
    const start = page * pageSize;
    return sorted.slice(start, start + pageSize);
  }, [sorted, page, pageSize]);

  return {
    rows: paginated,
    totalPages: Math.ceil(sorted.length / pageSize),
    page,
    setPage,
    setFilter,
    sortBy: (key) => setSortConfig(prev => ({
      key,
      direction: prev.key === key && prev.direction === 'asc' ? 'desc' : 'asc'
    })),
    sortConfig
  };
}

// С виртуализацией через react-window
function VirtualTable({ data, columns, rowHeight = 40 }) {
  const table = useTable({ data, columns, pageSize: data.length });

  return (
    <FixedSizeList
      height={400}
      itemCount={table.rows.length}
      itemSize={rowHeight}
    >
      {({ index, style }) => (
        <div style={style} className="table-row">
          {columns.map(col => (
            <span key={col.key}>{table.rows[index][col.key]}</span>
          ))}
        </div>
      )}
    </FixedSizeList>
  );
}
```
</details>

<details>
<summary><b>Реализуйте drag-and-drop без использования внешних библиотек</b></summary>

```javascript
function useDragAndDrop(items, onReorder) {
  const [draggedIndex, setDraggedIndex] = useState(null);

  const handleDragStart = (e, index) => {
    setDraggedIndex(index);
    e.dataTransfer.effectAllowed = 'move';
    e.dataTransfer.setData('text/plain', index);
  };

  const handleDragOver = (e, index) => {
    e.preventDefault();
    if (draggedIndex === null || draggedIndex === index) return;

    const newItems = [...items];
    const [draggedItem] = newItems.splice(draggedIndex, 1);
    newItems.splice(index, 0, draggedItem);

    setDraggedIndex(index);
    onReorder(newItems);
  };

  const handleDragEnd = () => {
    setDraggedIndex(null);
  };

  return { draggedIndex, handleDragStart, handleDragOver, handleDragEnd };
}

function DraggableList({ items, onReorder }) {
  const { draggedIndex, handleDragStart, handleDragOver, handleDragEnd } =
    useDragAndDrop(items, onReorder);

  return (
    <ul>
      {items.map((item, index) => (
        <li
          key={item.id}
          draggable
          onDragStart={(e) => handleDragStart(e, index)}
          onDragOver={(e) => handleDragOver(e, index)}
          onDragEnd={handleDragEnd}
          style={{
            opacity: draggedIndex === index ? 0.5 : 1,
            cursor: 'grab'
          }}
        >
          {item.text}
        </li>
      ))}
    </ul>
  );
}
```
</details>

<details>
<summary><b>Создайте динамический переключатель тем с CSS-переменными</b></summary>

```javascript
// Определения тем
const themes = {
  light: {
    '--bg-primary': '#ffffff',
    '--bg-secondary': '#f5f5f5',
    '--text-primary': '#1a1a1a',
    '--text-secondary': '#666666',
    '--accent': '#007bff',
  },
  dark: {
    '--bg-primary': '#1a1a1a',
    '--bg-secondary': '#2d2d2d',
    '--text-primary': '#ffffff',
    '--text-secondary': '#a0a0a0',
    '--accent': '#4dabf7',
  }
};

// Context и hook для темы
const ThemeContext = createContext();

function ThemeProvider({ children }) {
  const [theme, setTheme] = useState(() =>
    localStorage.getItem('theme') || 'light'
  );

  useEffect(() => {
    const root = document.documentElement;
    Object.entries(themes[theme]).forEach(([property, value]) => {
      root.style.setProperty(property, value);
    });
    localStorage.setItem('theme', theme);
  }, [theme]);

  const toggle = () => setTheme(t => t === 'light' ? 'dark' : 'light');

  return (
    <ThemeContext.Provider value={{ theme, toggle, setTheme }}>
      {children}
    </ThemeContext.Provider>
  );
}

const useTheme = () => useContext(ThemeContext);

// Использование в компонентах
function ThemeToggle() {
  const { theme, toggle } = useTheme();
  return <button onClick={toggle}>{theme === 'light' ? '🌙' : '☀️'}</button>;
}
```

**Использование в CSS:**
```css
body {
  background: var(--bg-primary);
  color: var(--text-primary);
}
.card { background: var(--bg-secondary); }
.link { color: var(--accent); }
```
</details>

<details>
<summary><b>Рендер 10k элементов эффективно с intersection observer + виртуализация</b></summary>

```javascript
function useIntersectionObserver(callback, options) {
  const targetRef = useRef(null);

  useEffect(() => {
    const observer = new IntersectionObserver(callback, options);
    if (targetRef.current) observer.observe(targetRef.current);
    return () => observer.disconnect();
  }, [callback, options]);

  return targetRef;
}

function VirtualizedList({ items, itemHeight = 40, overscan = 5 }) {
  const containerRef = useRef(null);
  const [scrollTop, setScrollTop] = useState(0);
  const [containerHeight, setContainerHeight] = useState(0);

  useEffect(() => {
    const container = containerRef.current;
    setContainerHeight(container.clientHeight);

    const handleScroll = () => setScrollTop(container.scrollTop);
    container.addEventListener('scroll', handleScroll);
    return () => container.removeEventListener('scroll', handleScroll);
  }, []);

  const totalHeight = items.length * itemHeight;
  const startIndex = Math.max(0, Math.floor(scrollTop / itemHeight) - overscan);
  const endIndex = Math.min(
    items.length,
    Math.ceil((scrollTop + containerHeight) / itemHeight) + overscan
  );

  const visibleItems = items.slice(startIndex, endIndex);

  return (
    <div
      ref={containerRef}
      style={{ height: '100%', overflow: 'auto' }}
    >
      <div style={{ height: totalHeight, position: 'relative' }}>
        {visibleItems.map((item, index) => (
          <div
            key={item.id}
            style={{
              position: 'absolute',
              top: (startIndex + index) * itemHeight,
              height: itemHeight,
              width: '100%'
            }}
          >
            {item.content}
          </div>
        ))}
      </div>
    </div>
  );
}

// С Intersection Observer для lazy loading изображений
function LazyImage({ src, alt }) {
  const [isVisible, setIsVisible] = useState(false);
  const ref = useIntersectionObserver(
    ([entry]) => entry.isIntersecting && setIsVisible(true),
    { threshold: 0.1 }
  );

  return (
    <div ref={ref}>
      {isVisible ? <img src={src} alt={alt} /> : <div className="placeholder" />}
    </div>
  );
}
```
</details>
