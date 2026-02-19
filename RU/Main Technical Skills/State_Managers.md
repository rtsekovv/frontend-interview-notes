# Вопросы для собеседования по State Managers

## Redux

<details>
<summary><b>Что такое Redux?</b></summary>

Предсказуемый контейнер состояния для JavaScript-приложений. Хранит всё состояние приложения в одном объекте (store). Состояние меняется через pure functions (reducers), вызываемые actions. Полезен для сложных приложений с shared state.
</details>

<details>
<summary><b>Что такое Flux?</b></summary>

Архитектурный паттерн от Facebook для однонаправленного потока данных. Компоненты: Dispatcher (центральный hub), Stores (хранят state), Views (React-компоненты), Actions (события). Данные текут в одном направлении: Action → Dispatcher → Store → View.
</details>

<details>
<summary><b>В чём разница между Redux и Flux?</b></summary>

- Redux: Один store, reducers — pure functions, нет dispatcher
- Flux: Несколько stores, stores содержат логику, есть dispatcher

Redux проще и более предсказуем.
</details>

<details>
<summary><b>Назовите основные принципы Redux?</b></summary>

- **Single source of truth**: Один store для всего состояния приложения
- **State is read-only**: Единственный способ изменить — dispatch action
- **Changes via pure functions**: Reducers — pure functions (state, action) → newState
</details>

<details>
<summary><b>Что вы понимаете под action в архитектуре Redux?</b></summary>

Action — простой объект, описывающий что произошло. Обязательно имеет свойство `type`. Может иметь `payload` с данными. Пример: `{ type: 'ADD_TODO', payload: { text: 'Learn Redux' } }`. Dispatched для инициации изменений состояния.
</details>

## Redux Toolkit

<details>
<summary><b>Как работает Redux Toolkit?</b></summary>

Официальный набор инструментов Redux, упрощающий настройку. `configureStore()` настраивает store с хорошими defaults. `createSlice()` генерирует actions и reducers. Включает Immer (пишите "мутирующую" логику), RTK Query для data fetching. Меньше boilerplate.
</details>

<details>
<summary><b>Можете объяснить назначение Redux middleware? Какие популярные middleware библиотеки используются с Redux?</b></summary>

Middleware перехватывает actions до достижения reducer. Используется для: logging, async операций, обработки ошибок. Популярные: Redux Thunk (простой async), Redux Saga (сложный async с generators), Redux Logger (отладка).
</details>

<details>
<summary><b>Можете объяснить концепцию immutability в Redux? Почему важно поддерживать immutability при работе с Redux store?</b></summary>

Никогда не изменяйте объект state напрямую. Создавайте новый объект с изменениями. Важно потому что: включает time-travel debugging, предсказуемые изменения состояния, React может обнаружить изменения через сравнение ссылок. Redux Toolkit использует Immer для автоматической обработки этого.
</details>

<details>
<summary><b>Можете описать разницу между combineReducers и createSlice в Redux Toolkit? Когда бы вы выбрали один вместо другого?</b></summary>

- `combineReducers`: Объединяет несколько reducer functions в один. Используется когда есть отдельные reducers для разных slices состояния
- `createSlice`: Создаёт reducer + actions для одного slice. Включает Immer, генерирует action creators

Используйте `createSlice` для нового кода. Используйте `combineReducers` для объединения нескольких slices.
</details>

## MobX

<details>
<summary><b>В чём разница между MobX и Redux?</b></summary>

- **Redux**: Один store, явные обновления через actions/reducers, больше boilerplate, предсказуемый
- **MobX**: Несколько stores, автоматические обновления через observables, меньше boilerplate, более "магический"

MobX проще, но менее предсказуем. Redux лучше для больших команд.
</details>

<details>
<summary><b>Как управлять state в MobX?</b></summary>

Пометьте state как `observable`, компоненты как `observer`. Когда observable меняется, observers автоматически re-render. Используйте `makeObservable` или `makeAutoObservable` в class/store. Изменения state происходят в `action` методах.
</details>

<details>
<summary><b>Какова цель MobX action function?</b></summary>

Actions — методы, модифицирующие state. Помечайте декоратором `@action` или `action()`. Преимущества: батчит несколько изменений state в одно обновление, включает отслеживание транзакций, обязателен в strict mode.
</details>

<details>
<summary><b>Как обрабатывать асинхронные операции в MobX?</b></summary>

Используйте `flow` для async операций с generators. Или используйте обычный async/await, но оборачивайте модификации state в `runInAction()`. `flow` обеспечивает лучшее отслеживание и поддержку отмены.
</details>

<details>
<summary><b>Какова роль observables в MobX? Как они обеспечивают автоматические обновления state?</b></summary>

Observables отслеживают значения state. MobX отслеживает какие observables каждый компонент использует при render. Когда observable меняется, MobX автоматически re-render только компоненты, использующие это значение. Ручная подписка не нужна.
</details>

<details>
<summary><b>Что такое actions в MobX и почему они важны? Как они обеспечивают корректное отслеживание мутаций state?</b></summary>

Actions оборачивают модификации state. Важны: батчат обновления (один re-render для нескольких изменений), включают debugging/logging, обязательны в strict mode. Все изменения state должны происходить внутри actions.
</details>

<details>
<summary><b>Как MobX обрабатывает асинхронные операции? Знакомы ли вы с MobX flow и как он помогает управлять async flows?</b></summary>

`flow` использует generator functions для async. Преимущества: модификации state автоматически оборачиваются в actions, поддерживает отмену, лучшие stack traces. Альтернатива: использовать async/await с `runInAction()` для обновлений state.
</details>

## GraphQL и React-Query

<details>
<summary><b>Что такое GraphQL и чем он отличается от RESTful APIs?</b></summary>

- **GraphQL**: Один endpoint, клиент указывает точно какие данные нужны, строгая типизация, вложенные данные в одном запросе
- **REST**: Несколько endpoints, сервер определяет форму ответа, over/under fetching распространены

GraphQL уменьшает сетевые запросы и даёт гибкость клиенту.
</details>

<details>
<summary><b>Что такое GraphQL mutations и чем они отличаются от queries?</b></summary>

- **Queries**: Чтение данных (эквивалент GET)
- **Mutations**: Изменение данных (эквивалент POST/PUT/DELETE)

Mutations имеют побочные эффекты, queries нет. Оба используют похожий синтаксис, но разные keywords.
</details>

<details>
<summary><b>Опишите основные компоненты React Query: Queries, Mutations и Query Caching?</b></summary>

- **Queries** (`useQuery`): Получение данных, автоматическое кэширование/refetching
- **Mutations** (`useMutation`): Изменение данных, инвалидация cache после
- **Query Cache**: Хранит полученные данные, настраиваемое stale time, фоновые обновления

Также: devtools, prefetching, поддержка пагинации.
</details>

<details>
<summary><b>Можете объяснить концепцию query keys в React Query? Как бы вы использовали их для управления и ссылок на queries?</b></summary>

Query keys идентифицируют и кэшируют queries. Формат массива: `['todos', { status: 'done' }]`. Используются для: lookup в cache, инвалидации, refetching конкретных queries. Иерархические — можно инвалидировать все 'todos' queries сразу.
</details>

## Redux Thunk

<details>
<summary><b>Как обрабатывать асинхронные actions в Redux? Знакомы ли вы с Redux Thunk или Redux Saga? Можете объяснить как они работают?</b></summary>

- **Redux Thunk**: Middleware, позволяющий actions возвращать функции вместо объектов. Функция получает dispatch и getState. Прост для базового async
- **Redux Saga**: Использует generators для сложных async flows. Более мощный, но более сложный
</details>

<details>
<summary><b>Как Redux Thunk обеспечивает обработку асинхронных API calls? Можете объяснить flow dispatch thunk action и его выполнения?</b></summary>

Flow:
1. Dispatch thunk (функция)
2. Middleware перехватывает её (не простой объект)
3. Middleware вызывает функцию с (dispatch, getState)
4. Внутри функции: dispatch loading action → делаем API call → dispatch success/error action
</details>

## Redux Saga

<details>
<summary><b>В чём главное отличие Redux Thunk и Redux Saga в обработке асинхронных actions?</b></summary>

- **Thunk**: Простой, использует functions/promises, хорош для простого async
- **Saga**: Использует generators, декларативные effects, лучше для сложных flows (race conditions, отмена, retry logic)

У Saga круче learning curve, но более мощный.
</details>

<details>
<summary><b>Знакомы ли вы с effect creators Redux Saga типа take, put, call и fork? Можете объяснить их назначение и привести примеры использования?</b></summary>

- `take`: Ожидание конкретного action
- `put`: Dispatch action
- `call`: Вызов async function (blocking)
- `fork`: Вызов function non-blocking (параллельно)
- `select`: Получение state
- `takeEvery`/`takeLatest`: Обработка повторяющихся actions
</details>

<details>
<summary><b>Можете описать как Redux Saga обрабатывает сложные сценарии control flow, такие как race conditions, параллельные вызовы или отмена tasks?</b></summary>

- **Race**: `race([call(api1), call(api2)])` — первый завершившийся выигрывает
- **Parallel**: `all([call(api1), call(api2)])` — ждём все
- **Cancellation**: `fork` возвращает task, отмена через `cancel(task)`
- **Debounce**: `debounce(ms, ACTION, saga)`

Generators делают сложные flows читаемыми.
</details>
