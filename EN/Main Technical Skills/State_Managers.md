# State Managers Interview Questions

## Redux

<details>
<summary><b>What is Redux?</b></summary>

Predictable state container for JavaScript apps. Stores entire app state in single object (store). State changes through pure functions (reducers) triggered by actions. Useful for complex apps with shared state.
</details>

<details>
<summary><b>What is Flux?</b></summary>

Architecture pattern by Facebook for unidirectional data flow. Components: Dispatcher (central hub), Stores (hold state), Views (React components), Actions (events). Data flows one way: Action → Dispatcher → Store → View.
</details>

<details>
<summary><b>What is the difference between Redux and Flux?</b></summary>

- Redux: Single store, reducers are pure functions, no dispatcher
- Flux: Multiple stores, stores contain logic, has dispatcher

Redux is simpler and more predictable.
</details>

<details>
<summary><b>State the core principles of Redux?</b></summary>

- **Single source of truth**: One store for entire app state
- **State is read-only**: Only way to change is dispatching action
- **Changes via pure functions**: Reducers are pure functions (state, action) → newState
</details>

<details>
<summary><b>What do you understand by an action in Redux's architecture?</b></summary>

Action is plain object describing what happened. Must have `type` property. Can have `payload` with data. Example: `{ type: 'ADD_TODO', payload: { text: 'Learn Redux' } }`. Dispatched to trigger state changes.
</details>

## Redux Toolkit

<details>
<summary><b>How does Redux Toolkit work?</b></summary>

Official Redux toolset that simplifies setup. `configureStore()` sets up store with good defaults. `createSlice()` generates actions and reducers. Includes Immer (write "mutating" logic), RTK Query for data fetching. Less boilerplate.
</details>

<details>
<summary><b>Can you explain the purpose of Redux middleware? What are some popular middleware libraries used with Redux?</b></summary>

Middleware intercepts actions before reaching reducer. Used for: logging, async operations, error handling. Popular: Redux Thunk (simple async), Redux Saga (complex async with generators), Redux Logger (debugging).
</details>

<details>
<summary><b>Can you explain the concept of immutability in Redux? Why is it important to maintain immutability when working with the Redux store?</b></summary>

Never directly modify state object. Create new object with changes. Important because: enables time-travel debugging, predictable state changes, React can detect changes via reference comparison. Redux Toolkit uses Immer to handle this automatically.
</details>

<details>
<summary><b>Can you describe the difference between combineReducers and createSlice in Redux Toolkit? When would you choose to use one over the other?</b></summary>

- `combineReducers`: Combines multiple reducer functions into one. Used when you have separate reducers for different state slices
- `createSlice`: Creates reducer + actions for one slice. Includes Immer, generates action creators

Use `createSlice` for new code. Use `combineReducers` to combine multiple slices.
</details>

## MobX

<details>
<summary><b>What is the difference between MobX and Redux?</b></summary>

- **Redux**: Single store, explicit updates via actions/reducers, more boilerplate, predictable
- **MobX**: Multiple stores, automatic updates via observables, less boilerplate, more magical

MobX is simpler but less predictable. Redux better for large teams.
</details>

<details>
<summary><b>How do you handle state management in MobX?</b></summary>

Mark state as `observable`, components as `observer`. When observable changes, observers automatically re-render. Use `makeObservable` or `makeAutoObservable` in class/store. State changes happen in `action` methods.
</details>

<details>
<summary><b>What is the purpose of the MobX action function?</b></summary>

Actions are methods that modify state. Mark with `@action` decorator or `action()`. Benefits: batches multiple state changes into one update, enables transaction tracking, required in strict mode.
</details>

<details>
<summary><b>How do you handle asynchronous operations in MobX?</b></summary>

Use `flow` for async operations with generators. Or use regular async/await but wrap state modifications in `runInAction()`. `flow` provides better tracking and cancellation support.
</details>

<details>
<summary><b>What is the role of observables in MobX? How do they enable automatic state updates?</b></summary>

Observables track state values. MobX tracks which observables each component uses during render. When observable changes, MobX automatically re-renders only components that use that value. No manual subscription needed.
</details>

<details>
<summary><b>What are actions in MobX, and why are they important? How do they ensure that state mutations are tracked correctly?</b></summary>

Actions wrap state modifications. Important: batch updates (one re-render for multiple changes), enable debugging/logging, required in strict mode. All state changes should happen inside actions.
</details>

<details>
<summary><b>How does MobX handle asynchronous operations? Are you familiar with the MobX flow and how it helps manage async flows?</b></summary>

`flow` uses generator functions for async. Advantages: state modifications automatically wrapped in actions, supports cancellation, better stack traces. Alternative: use async/await with `runInAction()` for state updates.
</details>

## GraphQL & React-Query

<details>
<summary><b>What is GraphQL and how does it differ from RESTful APIs?</b></summary>

- **GraphQL**: Single endpoint, client specifies exact data needed, strong typing, nested data in one request
- **REST**: Multiple endpoints, server decides response shape, over/under fetching common

GraphQL reduces network requests and gives flexibility to client.
</details>

<details>
<summary><b>What are GraphQL mutations, and how do they differ from queries?</b></summary>

- **Queries**: Read data (GET equivalent)
- **Mutations**: Modify data (POST/PUT/DELETE equivalent)

Mutations have side effects, queries don't. Both use similar syntax but different keywords.
</details>

<details>
<summary><b>Describe the main components of React Query, such as Queries, Mutations, and Query Caching?</b></summary>

- **Queries** (`useQuery`): Fetch data, automatic caching/refetching
- **Mutations** (`useMutation`): Modify data, invalidate cache after
- **Query Cache**: Stores fetched data, configurable stale time, background updates

Also: devtools, prefetching, pagination support.
</details>

<details>
<summary><b>Can you explain the concept of query keys in React Query? How would you use them to manage and reference queries?</b></summary>

Query keys identify and cache queries. Array format: `['todos', { status: 'done' }]`. Used for: cache lookup, invalidation, refetching specific queries. Hierarchical - can invalidate all 'todos' queries at once.
</details>

## Redux Thunk

<details>
<summary><b>How to handle asynchronous actions in Redux? Are you familiar with Redux Thunk or Redux Saga? Can you explain how they work?</b></summary>

- **Redux Thunk**: Middleware that lets actions return functions instead of objects. Function receives dispatch and getState. Simple for basic async
- **Redux Saga**: Uses generators for complex async flows. More powerful but more complex
</details>

<details>
<summary><b>How does Redux Thunk enable handling asynchronous API calls? Can you explain the flow of dispatching a thunk action and its execution?</b></summary>

Flow:
1. Dispatch thunk (function)
2. Middleware catches it (not plain object)
3. Middleware calls function with (dispatch, getState)
4. Inside function: dispatch loading action → make API call → dispatch success/error action
</details>

## Redux Saga

<details>
<summary><b>What is the main difference between Redux Thunk and Redux Saga in terms of handling asynchronous actions?</b></summary>

- **Thunk**: Simple, uses functions/promises, good for simple async
- **Saga**: Uses generators, declarative effects, better for complex flows (race conditions, cancellation, retry logic)

Saga has steeper learning curve but more powerful.
</details>

<details>
<summary><b>Are you familiar with Redux Saga's effect creators like take, put, call, and fork? Can you explain their purposes and provide examples of their usage?</b></summary>

- `take`: Wait for specific action
- `put`: Dispatch action
- `call`: Call async function (blocking)
- `fork`: Call function non-blocking (parallel)
- `select`: Get state
- `takeEvery`/`takeLatest`: Handle repeated actions
</details>

<details>
<summary><b>Can you describe how Redux Saga handles complex control flow scenarios, such as race conditions, parallel calls, or cancellation of tasks?</b></summary>

- **Race**: `race([call(api1), call(api2)])` - first to finish wins
- **Parallel**: `all([call(api1), call(api2)])` - wait for all
- **Cancellation**: `fork` returns task, cancel with `cancel(task)`
- **Debounce**: `debounce(ms, ACTION, saga)`

Generators make complex flows readable.
</details>
