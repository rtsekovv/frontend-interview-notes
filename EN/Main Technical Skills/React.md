# React Interview Questions

## Create React App & Setup

<details>
<summary><b>How to utilize CRA and what benefits it provides?</b></summary>

Run `npx create-react-app my-app`. Benefits: zero configuration, webpack/babel pre-configured, hot reloading, testing setup, optimized production build. Good for learning and small-medium projects.
</details>

<details>
<summary><b>What are some advantages of using Create React App for bootstrapping a React project compared to setting up the project from scratch?</b></summary>

No webpack/babel configuration needed, best practices built-in, easy updates via react-scripts, includes testing tools (Jest), consistent project structure, fast start. Manual setup gives more control but takes time.
</details>

<details>
<summary><b>How does React handle events?</b></summary>

React uses SyntheticEvents - wrapper around native events for cross-browser consistency. camelCase naming (`onClick`). Pass function reference, not call (`onClick={handleClick}`, not `onClick={handleClick()}`). Events pooled for performance.
</details>

<details>
<summary><b>What are the challenges or limitations while using Create React App?</b></summary>

Limited customization without ejecting, no SSR support, can't modify webpack directly, may include unused code, ejecting is one-way. Alternatives: Next.js, Vite, custom setup.
</details>

## Architecture & Project Structure

<details>
<summary><b>Explain the concept of component-based architecture in React</b></summary>

UI built from reusable, independent components. Each component handles own rendering and logic. Components compose into larger components. Benefits: reusability, isolation, easier testing, parallel development.
</details>

<details>
<summary><b>How do you typically organize the folder structure in a React project?</b></summary>

Common structure:
- `src/`: All source code
- `components/`: Reusable UI components
- `pages/` or `views/`: Route-level components
- `hooks/`: Custom hooks
- `utils/`: Helper functions
- `services/`: API calls
- `context/` or `store/`: State management
</details>

<details>
<summary><b>What approaches do you use when developing an architecture in an application?</b></summary>

Consider: separation of concerns, component hierarchy, state management strategy, folder structure (feature-based vs type-based), styling approach, testing strategy. Document decisions. Keep it simple initially, refactor as needed.
</details>

<details>
<summary><b>What are the advantages of Fractal architecture?</b></summary>

Each feature folder contains everything it needs (components, hooks, tests, styles). Self-contained modules. Benefits: easy to find related code, portable features, scales well, clear boundaries.
</details>

<details>
<summary><b>What are the advantages of Atomic design?</b></summary>

Components organized by complexity: atoms (button, input) → molecules (search field) → organisms (header) → templates → pages. Benefits: consistent design system, clear hierarchy, reusable primitives.
</details>

## Environment Setup

<details>
<summary><b>What are the necessary tools and dependencies required to set up a local development environment for a React project?</b></summary>

Node.js and npm/yarn, code editor (VS Code), React DevTools browser extension, Git. Optional: ESLint, Prettier, TypeScript. For CRA, just Node.js needed - everything else included.
</details>

<details>
<summary><b>How do you manage environment variables in a React project?</b></summary>

Use `.env` files (`.env.development`, `.env.production`). Variables must start with `REACT_APP_`. Access via `process.env.REACT_APP_*`. Never commit secrets - use `.env.local` for sensitive data.
</details>

<details>
<summary><b>What tools or techniques do you use to debug and troubleshoot issues in a React application?</b></summary>

React DevTools (inspect components, state, props), browser DevTools (console, network, breakpoints), console.log strategically, Redux DevTools for state. Error boundaries for catching errors.
</details>

<details>
<summary><b>What are the additional configurations or setup steps you typically perform to optimize the local development workflow?</b></summary>

ESLint + Prettier for code quality, husky for pre-commit hooks, path aliases for cleaner imports, VS Code extensions (ES7 snippets), TypeScript for type safety, hot reloading configuration.
</details>

## Routing & Navigation

<details>
<summary><b>How would you implement routing in a React application?</b></summary>

React Router is standard. Install `react-router-dom`. Wrap app in `BrowserRouter`. Use `Routes` and `Route` components. `Link` for navigation. Supports nested routes, params, query strings.
</details>

<details>
<summary><b>How would you handle 404 page not found scenarios in React Router?</b></summary>

Add catch-all route at end: `<Route path="*" element={<NotFound />} />`. Matches anything not matched by previous routes.
</details>

<details>
<summary><b>What are React Router hooks?</b></summary>

v6 hooks: `useNavigate()` (replaces useHistory), `useParams()`, `useLocation()`, `useSearchParams()`. Example:
```javascript
const navigate = useNavigate();
navigate('/dashboard'); // redirect
navigate(-1); // go back
```
</details>

<details>
<summary><b>How would you implement protected routes?</b></summary>

Create ProtectedRoute component that checks auth status. If not authenticated, redirect to login. Example:
```javascript
const ProtectedRoute = ({ children }) => {
  const isAuth = useAuth();
  return isAuth ? children : <Navigate to="/login" />;
};
```
</details>

## Data Management

<details>
<summary><b>What is the difference between controlled components and uncontrolled components in React?</b></summary>

- **Controlled**: React state controls input value. `value` + `onChange` handler. React is source of truth
- **Uncontrolled**: DOM controls value. Use `ref` to access. `defaultValue` for initial value

Controlled preferred - more predictable.
</details>

<details>
<summary><b>How would you handle asynchronous data fetching in React?</b></summary>

Use `useEffect` for fetch on mount. Manage loading/error states. Consider libraries: React Query, SWR (caching, refetching, deduplication). async/await in useEffect needs cleanup for race conditions.
</details>

<details>
<summary><b>How would you manage shared or global state between different components?</b></summary>

Options: lift state up, Context API (built-in, good for simple cases), Redux (complex apps), Zustand (simple API), Jotai/Recoil (atomic). Choose based on complexity and team familiarity.
</details>

<details>
<summary><b>What is the difference between server state and application state?</b></summary>

- **Server state**: Data stored on the server or external services, typically fetched via APIs. Examples: user profile from database, products list, comments. Characteristics: async, can be stale, needs caching strategy.

- **Application state**: Data specific to user's interaction with the application. Examples: UI state (modals, tabs), user preferences, form inputs, client-side filters. Characteristics: synchronous, local, temporary.

**Tools for each:**
- Server state: React Query, SWR, Apollo Client
- Application state: useState, useReducer, Zustand, Redux
</details>

<details>
<summary><b>What is the recommended way to consume external data in React?</b></summary>

Use **useEffect** hook to fetch data when component mounts or when dependencies change. Store fetched data in state using useState or useReducer.

**Libraries:**
- **REST APIs**: axios, fetch, React Query, SWR
- **GraphQL APIs**: Apollo Client, Relay, urql

**Modern approaches:**
- **React Query / SWR**: Caching, refetching, deduplication built-in
- **tRPC (T3 Stack)**: End-to-end type-safe APIs
- **Server Components (Next.js)**: Fetch data on server, no client-side fetching needed

```javascript
// Traditional approach
useEffect(() => {
  fetch('/api/data').then(res => res.json()).then(setData);
}, []);

// React Query approach
const { data, isLoading } = useQuery(['data'], fetchData);
```
</details>

## SEO

<details>
<summary><b>What is SEO and why it is important for a website?</b></summary>

Search Engine Optimization - making site discoverable by search engines. Important for: organic traffic, visibility, credibility. Involves: good content, meta tags, performance, mobile-friendly, semantic HTML.
</details>

<details>
<summary><b>How do you ensure that a Single-Page Application built with React is search engine friendly?</b></summary>

Use SSR (Next.js) or SSG for pre-rendered HTML. Add meta tags (react-helmet). Implement proper routing. Use semantic HTML. Create sitemap. Ensure fast load times.
</details>

<details>
<summary><b>What is the SPA?</b></summary>

Single Page Application - loads once, updates content dynamically without full page reloads. JavaScript handles routing. Faster navigation after initial load. Examples: Gmail, Facebook.
</details>

<details>
<summary><b>What are the main problems of SPA with SEO?</b></summary>

Search engines may not execute JavaScript. Empty initial HTML. Slow time to content. Dynamic meta tags not seen. Social media sharing issues (no preview).
</details>

<details>
<summary><b>What are the solutions?</b></summary>

Server-Side Rendering (SSR), Static Site Generation (SSG), prerendering services, dynamic rendering for bots. Next.js/Gatsby solve this. Proper meta tags with react-helmet-async.
</details>

<details>
<summary><b>In which cases is it worth building an SPA?</b></summary>

SPAs are ideal for:
- **Mobile app-like experience and PWA**: Smooth transitions, offline support
- **Complex state management**: Persistent state across views, real-time updates
- **Highly interactive UIs**: No page reloads, faster view transitions
- **Dashboard applications**: Heavy user interaction, frequent updates
- **Applications behind authentication**: SEO less important

Avoid SPA for: content-heavy sites needing SEO, simple informational websites, blogs.
</details>

<details>
<summary><b>What is a meta-framework in the context of web development?</b></summary>

A meta-framework is a framework built on top of other frameworks or libraries, providing additional features and conventions.

**Examples:**
- **Next.js** → built on React.js (adds SSR, routing, API routes)
- **Nuxt.js** → built on Vue.js
- **Remix** → built on React (alternative to Next.js)
- **SvelteKit** → built on Svelte
- **NestJS** → built on Express/Fastify (backend)

Meta-frameworks provide: file-based routing, SSR/SSG, API routes, optimization, deployment solutions.
</details>

<details>
<summary><b>How can a React application be deployed without any meta-framework?</b></summary>

Steps for deploying a pure React SPA:

1. **Build script**: Add build script in package.json (`npm run build`)
2. **Choose provider**: Select hosting that supports SPAs (Netlify, Vercel, AWS S3 + CloudFront, GitHub Pages)
3. **Deploy**: Via CLI, FTP, or git remote repository
4. **Generate build**: Run `npm run build` to create production bundle
5. **Configure server**: Point to build directory (usually `dist` or `build`)
6. **Handle routing**: Configure redirects for client-side routing (redirect all routes to index.html)

```json
// _redirects file for Netlify
/*    /index.html   200
```
</details>

## Forms

<details>
<summary><b>How do you handle form submissions in React?</b></summary>

Add `onSubmit` to form element. Call `e.preventDefault()` to stop page reload. Access form data from state (controlled) or FormData API. Example:
```javascript
const handleSubmit = (e) => { e.preventDefault(); // process data };
```
</details>

<details>
<summary><b>How would you perform form validation in a React application?</b></summary>

Options: manual validation in onChange/onSubmit, Yup schema validation, Zod for TypeScript. Libraries like Formik and React Hook Form have built-in validation integration.
</details>

<details>
<summary><b>Can you explain the purpose of the onChange event in React forms?</b></summary>

`onChange` fires on every input change. Update state with new value: `onChange={(e) => setName(e.target.value)}`. Keeps React state synced with input (controlled component).
</details>

<details>
<summary><b>Are you familiar with form libraries like Formik or React Hook Form?</b></summary>

- **Formik**: Declarative, handles validation/errors/touched, good for complex forms
- **React Hook Form**: Performance-focused (fewer re-renders), uncontrolled by default, smaller bundle

Use for: complex validation, many fields, dynamic forms.
</details>

<details>
<summary><b>How would you handle form reset or clearing the form input values in React?</b></summary>

Controlled: reset state to initial values. Can use `form.reset()` for uncontrolled. React Hook Form has `reset()` method. Formik has `resetForm()`.
</details>

<details>
<summary><b>How would you handle file uploads in a React form?</b></summary>

Use `<input type="file">`. Access file via `e.target.files[0]`. Send with FormData to backend. Consider: file size limits, allowed types, progress indicator, preview for images.
</details>

## Formik, YUP & React Hook Form

<details>
<summary><b>What are the advantages of Formik?</b></summary>

Reduces boilerplate, handles: values, errors, touched, validation, submission. Easy integration with Yup. `Field` and `ErrorMessage` components. Good documentation.
</details>

<details>
<summary><b>How to create a dynamic form with dynamic fields?</b></summary>

Use Formik's `FieldArray` for arrays of fields. Can add/remove fields dynamically. Access via `arrayHelpers.push()`, `arrayHelpers.remove(index)`.
</details>

<details>
<summary><b>How to add errors from the backend to the form?</b></summary>

Formik: use `setErrors()` or `setFieldError()` after API response. React Hook Form: `setError('fieldName', { message: 'error' })`.
</details>

<details>
<summary><b>How to validate form data?</b></summary>

Formik: `validate` function or `validationSchema` (Yup). React Hook Form: `resolver` with Yup/Zod or `rules` prop on register.
</details>

<details>
<summary><b>What are the advantages of YUP?</b></summary>

Declarative schema validation. Chainable methods. Built-in validators (email, url, min, max). Easy error messages. Works well with TypeScript. Schema reusable.
</details>

<details>
<summary><b>How to validate dynamic fields with YUP?</b></summary>

Use `Yup.array().of(schema)` for array fields. Each item validated against inner schema. Can add `min()`, `max()` for array length.
</details>

<details>
<summary><b>What are the advantages of React-hook-forms?</b></summary>

Performance (minimal re-renders), small bundle size, easy integration with UI libraries, built-in validation, TypeScript support, uncontrolled inputs by default.
</details>

<details>
<summary><b>What are the advantages of useFormContext?</b></summary>

Access form methods in nested components without prop drilling. Wrap form in `FormProvider`. Child components use `useFormContext()` to access register, errors, etc.
</details>

## Components & Lifecycle

<details>
<summary><b>What are the different phases of ReactJS component lifecycle?</b></summary>

Three phases:
- **Mounting**: constructor, render, componentDidMount (useEffect with [])
- **Updating**: render, componentDidUpdate (useEffect with deps)
- **Unmounting**: componentWillUnmount (useEffect cleanup)
</details>

<details>
<summary><b>Explain the difference between functional and class components.</b></summary>

- **Class**: ES6 class, `this.state`, lifecycle methods, more verbose
- **Functional**: Plain functions, hooks for state/effects, simpler, preferred now

Functional components with hooks are modern standard.
</details>

<details>
<summary><b>What's the difference between an Element and a Component in React?</b></summary>

- **Element**: Plain object describing what to render. Immutable. Created by JSX: `<div>Hello</div>`
- **Component**: Function or class that returns elements. Reusable, can have state/props
</details>

<details>
<summary><b>How would you clean up resources or perform cleanup operations when using React Hooks?</b></summary>

Return function from useEffect runs on cleanup:
```javascript
useEffect(() => {
  const subscription = subscribe();
  return () => subscription.unsubscribe(); // cleanup
}, []);
```
Runs before next effect and on unmount.
</details>

## Virtual DOM & Reconciliation

<details>
<summary><b>What is the difference between DOM and virtual DOM in React.js?</b></summary>

- **DOM**: Browser's representation of HTML. Slow to update directly
- **Virtual DOM**: JavaScript copy of DOM. React updates virtual first, diffs with real DOM, updates only changed parts (efficient)
</details>

<details>
<summary><b>Explain the basis of React Reconciliation</b></summary>

Reconciliation is diffing algorithm. Compares old and new virtual DOM. Rules: different types = rebuild, same type = update attributes, keys help identify list items. Minimizes actual DOM operations.
</details>

<details>
<summary><b>What is the difference between ShadowDOM and VirtualDOM?</b></summary>

- **Shadow DOM**: Browser feature for encapsulation. Hides internal structure. Used by Web Components
- **Virtual DOM**: JavaScript abstraction for efficient updates. React concept

Different purposes - isolation vs performance.
</details>

<details>
<summary><b>What is React Fiber and why was it introduced?</b></summary>

Fiber is React's reconciliation engine (React 16+). Reimplements core algorithm for:
- Incremental rendering: split work into chunks
- Pause, abort, or reuse work
- Priority-based updates
- Better support for animations and gestures

Enables concurrent features like Suspense and transitions.
</details>

<details>
<summary><b>What is Concurrent Rendering?</b></summary>

React can work on multiple versions of UI simultaneously. Allows:
- Interruptible rendering (urgent updates don't wait for expensive ones)
- Automatic batching
- Transitions (mark updates as non-urgent)
- Suspense for data fetching

Enabled with React 18's createRoot.
</details>

## Refs

<details>
<summary><b>Refs should be used in the following cases - explain</b></summary>

Use refs for: DOM access (focus, scroll, measure), integrating with third-party libraries, storing mutable values that don't trigger re-render, keeping reference to intervals/timeouts.
</details>

<details>
<summary><b>What is the difference between useRef and createRef?</b></summary>

- `useRef`: Hook, persists across renders, returns same object
- `createRef`: Creates new ref each call, for class components

In functional components, always use `useRef`.
</details>

## Hooks

<details>
<summary><b>What are the rules of hooks?</b></summary>

1. Only call hooks at top level (not inside loops, conditions, nested functions)
2. Only call hooks from React functions (components or custom hooks)

Rules exist because React relies on call order to associate state with hooks. Breaking order causes bugs.
</details>

<details>
<summary><b>Why can't hooks be called conditionally?</b></summary>

React tracks hooks by their call order during each render. If you call hooks conditionally, the order changes between renders, and React can't match state to the correct hook. Always call all hooks, then use conditions inside.
</details>

<details>
<summary><b>What happens if you omit the dependency array in useEffect?</b></summary>

Effect runs after every render. This can cause performance issues or infinite loops if effect updates state. Always specify dependencies unless you intentionally want to run on every render.
</details>

<details>
<summary><b>What is the difference between useEffect and useLayoutEffect?</b></summary>

- `useEffect`: Runs asynchronously after browser paints. Non-blocking. Use for most side effects
- `useLayoutEffect`: Runs synchronously after DOM mutations, before paint. Blocks visual updates

Use `useLayoutEffect` only when you need to measure/mutate DOM before user sees it (tooltips, animations).
</details>

<details>
<summary><b>When should you NOT use useMemo?</b></summary>

Don't use when:
- Computation is cheap (simple math, string concat)
- Value changes on most renders anyway
- Premature optimization (profile first)

useMemo has overhead (comparison, memory). Only use for expensive calculations that don't change often.
</details>

<details>
<summary><b>Can you store non-DOM values in useRef?</b></summary>

Yes. useRef can store any mutable value that persists across renders without causing re-render. Use for: previous values, timer IDs, instance variables, any value you need to keep but not in state.
```javascript
const renderCount = useRef(0);
renderCount.current++;
```
</details>

<details>
<summary><b>What is useImperativeHandle and when would you use it?</b></summary>

Customizes the instance value exposed when using `ref` on a component with `forwardRef`. Use sparingly — only when you need to expose imperative methods to parent:
```javascript
useImperativeHandle(ref, () => ({
  focus: () => inputRef.current.focus(),
  clear: () => inputRef.current.value = ''
}));
```
</details>

<details>
<summary><b>What are useTransition and useDeferredValue?</b></summary>

React 18 concurrent features for non-urgent updates:
- `useTransition`: Mark state update as non-urgent, keep UI responsive
- `useDeferredValue`: Defer updating a value, show stale data during transitions

Use for expensive renders (filtering large lists) while keeping input responsive.
</details>

<details>
<summary><b>What are advantages of using React Hooks?</b></summary>

Simpler code, share stateful logic (custom hooks), no class complexity, better TypeScript support, easier testing, colocation of related logic, no lifecycle method confusion.
</details>

<details>
<summary><b>What is the difference between useMemo and useCallback?</b></summary>

- `useMemo`: Memoizes computed value. Returns value
- `useCallback`: Memoizes function. Returns function

`useCallback(fn, deps)` equals `useMemo(() => fn, deps)`.
</details>

<details>
<summary><b>Does React useState Hook update immediately?</b></summary>

No, state updates are batched and async. New value available on next render. To use new value immediately, use functional update: `setState(prev => prev + 1)`. Or useRef for immediate access.
</details>

<details>
<summary><b>Explain why the useState hook accepts a function as an initial value</b></summary>

When you pass a function to useState, it's called **lazy initialization**. The function is only executed once during the initial render, not on every re-render.

```javascript
// Expensive calculation runs on EVERY render
const [state, setState] = useState(expensiveCalculation());

// Expensive calculation runs only ONCE on initial render
const [state, setState] = useState(() => expensiveCalculation());
```

Use lazy initialization when:
- Initial value requires expensive computation
- Reading from localStorage/sessionStorage
- Parsing JSON or processing data
</details>

<details>
<summary><b>What is the difference between useState and useReducer?</b></summary>

- **useState**: Better for simple state management without complex logic. Single value or simple objects.
- **useReducer**: Designed for complex state logic with multiple sub-values, state transitions, and dispatch actions.

```javascript
// useState - simple state
const [count, setCount] = useState(0);

// useReducer - complex state with actions
const [state, dispatch] = useReducer(reducer, initialState);
dispatch({ type: 'INCREMENT' });
```

Use useReducer when: state logic is complex, next state depends on previous, multiple related values change together, you want predictable state transitions.
</details>

<details>
<summary><b>How to employ Reusable Hooks?</b></summary>

Extract common logic into custom hooks (prefix `use`). Return needed values/functions. Example: `useLocalStorage`, `useFetch`, `useDebounce`. Can be shared across components or projects.
</details>

## Performance & Re-rendering

<details>
<summary><b>Under what circumstances does a component re-render in React?</b></summary>

A component re-renders when:

1. **State changes**: When component's state is updated via setState
2. **Props change**: When component receives new props (even if values are the same by reference)
3. **Parent re-renders**: When parent component re-renders, children re-render by default
4. **Context changes**: When consumed context value changes via useContext
5. **Hooks with dependencies**: When useEffect, useMemo, useCallback dependencies change, the effect runs and may cause re-render
</details>

<details>
<summary><b>How can we prevent unnecessary re-renders?</b></summary>

1. **React.memo**: Wrap functional components to prevent re-render if props haven't changed
2. **useMemo**: Memoize expensive computed values
3. **useCallback**: Memoize callback functions passed as props
4. **Proper dependency arrays**: Configure hook dependencies correctly
5. **useRef for form values**: For large forms, prefer useRef over useState to avoid re-renders on every keystroke
6. **State colocation**: Keep state as close as possible to where it's used
</details>

<details>
<summary><b>What is the advantage of using React.memo API?</b></summary>

React.memo is a higher-order component that prevents unnecessary re-renders when the component's props haven't changed.

```javascript
const MyComponent = React.memo(function MyComponent({ name, count }) {
  return <div>{name}: {count}</div>;
});
```

**Benefits:**
- Improves performance by skipping re-renders
- Performs shallow comparison of props by default
- Can provide custom comparison function as second argument

**Use when:** Component renders often with same props, renders are expensive, component is pure (same props = same output).
</details>

<details>
<summary><b>What is virtualization? And what is it for?</b></summary>

Virtualization is a technique to optimize rendering of large lists or grids by only rendering visible items on the screen.

**Benefits:**
- Reduces number of DOM elements created and updated
- Minimizes memory usage
- Reduces layout calculations
- Enables smooth scrolling through thousands of items

**Libraries:** react-window, react-virtualized, TanStack Virtual

```javascript
import { FixedSizeList } from 'react-window';

<FixedSizeList height={400} itemCount={10000} itemSize={35} width={300}>
  {({ index, style }) => <div style={style}>Row {index}</div>}
</FixedSizeList>
```

Use virtualization for lists with 100+ items or when experiencing scroll performance issues.
</details>

## HOC & Advanced Patterns

<details>
<summary><b>What are advantages of using HOC?</b></summary>

Higher-Order Components: function that takes component, returns enhanced component. Benefits: reuse logic, cross-cutting concerns (auth, logging). Being replaced by custom hooks but still useful.
</details>

<details>
<summary><b>What is Prop-drilling in ReactJS?</b></summary>

Passing props through multiple component levels to reach deep child. Problems: verbose, hard to maintain. Solutions: Context API, state management libraries, component composition.
</details>

<details>
<summary><b>What is Lazy Loading in ReactJS?</b></summary>

Load components only when needed. Use `React.lazy()` + `Suspense`. Reduces initial bundle size. Good for routes, modals, heavy components.
```javascript
const LazyComponent = React.lazy(() => import('./Component'));
```
</details>

## State Management

<details>
<summary><b>How does Context cause performance issues?</b></summary>

Every component consuming context re-renders when context value changes, even if they only use part of it. Solutions: split into multiple contexts, memoize provider value, use state selectors (Zustand), or consider other state managers for frequent updates.
</details>

<details>
<summary><b>How do you prevent Context from causing unnecessary re-renders?</b></summary>

1. Split context by concern (UserContext, ThemeContext)
2. Memoize context value: `useMemo(() => ({ user }), [user])`
3. Use React.memo on consuming components
4. Consider selector-based state (Zustand, Jotai) for fine-grained updates
</details>

<details>
<summary><b>What are the alternatives to Redux in 2025?</b></summary>

- **Zustand**: Simple, minimal boilerplate, selector-based
- **Jotai**: Atomic state model, bottom-up approach
- **Valtio**: Proxy-based, mutable-style API
- **React Query/TanStack Query**: For server state
- **Recoil**: Facebook's atomic state (less active)

Choose based on: app complexity, team preference, bundle size concerns.
</details>

<details>
<summary><b>How does Redux Toolkit improve upon Redux?</b></summary>

- `createSlice`: Combines reducer + actions, uses Immer for immutable updates
- `configureStore`: Includes Redux DevTools and middleware by default
- `createAsyncThunk`: Simplified async actions
- RTK Query: Built-in data fetching/caching

Less boilerplate, better defaults, same Redux concepts.
</details>

<details>
<summary><b>What is optimistic UI updating?</b></summary>

Update UI immediately assuming success, revert if request fails. Better UX - feels instant. Implementation: update state, send request, rollback on error:
```javascript
const prev = state;
setState(optimisticValue);
try { await api.update(); } catch { setState(prev); }
```
</details>

## Events

<details>
<summary><b>Describe how events are handled in React.</b></summary>

React uses SyntheticEvent wrapper. camelCase names. Event handlers as props. Event pooling (reused). Access native event via `e.nativeEvent`. stopPropagation and preventDefault work normally.
</details>

<details>
<summary><b>What is a Synthetic event?</b></summary>

React's cross-browser wrapper around native events. Same interface across browsers. Automatically cleaned up. Access with event parameter in handler. Contains: target, currentTarget, type, etc.
</details>

## Next.js & SSR

<details>
<summary><b>What are Next.js benefits?</b></summary>

Benefits: SSR/SSG built-in, file-based routing, API routes, image optimization, automatic code splitting, TypeScript support, great developer experience. Good for SEO-critical apps.
</details>

<details>
<summary><b>What do you mean by SSR?</b></summary>

Server-Side Rendering - HTML generated on server for each request. User sees content immediately. Better SEO, faster perceived load. Trade-off: server load, TTFB can be slower.
</details>

<details>
<summary><b>What types of pre-rendering are available in Next JS?</b></summary>

Two types:
- **SSG** (Static Site Generation): HTML generated at build time
- **SSR** (Server-Side Rendering): HTML generated on each request

Also ISR (Incremental Static Regeneration) - rebuild pages in background.
</details>

<details>
<summary><b>Differentiate between the pre-rendering types available in Next JS?</b></summary>

- **SSG**: Best performance, use for static content. `getStaticProps`
- **SSR**: Always fresh data, use for dynamic content. `getServerSideProps`
- **ISR**: Best of both - static with revalidation. `revalidate` option
</details>

<details>
<summary><b>What are the properties available in a context object that arises on using serverSideProps?</b></summary>

Context contains: `params` (route parameters), `req` (request object), `res` (response object), `query` (query string), `preview` (preview mode status), `resolvedUrl`.
</details>

<details>
<summary><b>Explain the importance of code splitting in Next JS and dynamic import?</b></summary>

Code splitting reduces bundle size. Each page is separate chunk. Dynamic imports (`next/dynamic`) for components loaded on demand. Improves initial load time.
</details>

<details>
<summary><b>What is the purpose of the getStaticPaths function?</b></summary>

`getStaticPaths` is used when your dynamic page uses `getStaticProps`. Next.js needs to know all possible paths for your dynamic route at build time.

```javascript
// pages/posts/[id].js
export async function getStaticPaths() {
  const posts = await fetchPosts();
  return {
    paths: posts.map(post => ({ params: { id: post.id } })),
    fallback: false // or 'blocking' or true
  };
}
```

**Fallback options:**
- `false`: 404 for unknown paths
- `true`: Generate page on-demand, show loading state
- `'blocking'`: Generate on-demand, SSR-like behavior

You can use `getStaticProps` without `getStaticPaths` for non-dynamic routes.
</details>

<details>
<summary><b>How does the next/image API work? And why does it improve performance?</b></summary>

The `next/image` component optimizes images automatically:

1. **Server-side optimization**: Images resized, format converted (to WebP), and compressed
2. **Lazy loading**: Images load only when entering viewport
3. **Responsive sizing**: Serves appropriate size for device
4. **Caching**: Optimized images cached with headers for browser/CDN

```javascript
import Image from 'next/image';

<Image
  src="/photo.jpg"
  width={500}
  height={300}
  alt="Description"
  priority // for above-the-fold images
/>
```

**Performance benefits:** Smaller file sizes, faster page loads, better Core Web Vitals (LCP), prevents layout shift (CLS).
</details>

<details>
<summary><b>How would you deploy a Next.js application without hosting it on Vercel?</b></summary>

Next.js can be deployed on any platform supporting Node.js:

1. **Build**: `npm run build`
2. **Start**: `npm run start` (requires Node.js server)
3. **Platforms**: AWS EC2/ECS, DigitalOcean, Railway, Render, Docker containers, any VPS

**For static export** (no SSR):
```javascript
// next.config.js
module.exports = { output: 'export' }
```
Then deploy to any static hosting (S3, Netlify, GitHub Pages).

The only difference from Vercel is that you manage infrastructure yourself instead of having it automated.
</details>

<details>
<summary><b>How do API routes work in Next.js?</b></summary>

Next.js API routes provide built-in backend endpoints within your Next.js app. Create files inside `pages/api/` (or `app/api/` in App Router) - they become server-side functions.

```javascript
// pages/api/users.js
export default function handler(req, res) {
  if (req.method === 'GET') {
    res.status(200).json({ users: [] });
  } else if (req.method === 'POST') {
    // Create user
    res.status(201).json({ success: true });
  }
}
```

**Features:** Access to request/response objects, middleware support, can connect to databases, serverless deployment ready.
</details>

<details>
<summary><b>Can you use API Routes if the app is not hosted on Vercel?</b></summary>

Yes, Next.js API routes work on any platform supporting Node.js. They're not Vercel-specific.

**Requirements:**
- Node.js server running (not static export)
- `npm run build` + `npm run start`

Works on: AWS, DigitalOcean, Heroku, Railway, any VPS with Node.js. The runtime is the same regardless of hosting provider.
</details>

<details>
<summary><b>What is the advantage of using Serverless mode?</b></summary>

Serverless deployment for Next.js offers:

- **Improved scalability**: Functions automatically scale based on demand
- **Cost efficiency**: Pay only for compute resources actually used
- **Easier deployment**: No server management or infrastructure maintenance
- **Faster response times**: Functions deployed closer to users (edge locations)
- **Zero cold starts** (on Vercel): Optimized for Next.js

Best for: Variable traffic, cost-sensitive projects, global distribution needs.
</details>

<details>
<summary><b>Is it possible to use a static CDN with Next.js?</b></summary>

Yes, configure the `assetPrefix` option in `next.config.js`:

```javascript
// next.config.js
module.exports = {
  assetPrefix: 'https://cdn.example.com',
}
```

This prefixes all static assets (JS, CSS, images) with your CDN URL. The CDN serves static files while Next.js server handles SSR pages.

For fully static sites, use `output: 'export'` and deploy entire build to CDN.
</details>

<details>
<summary><b>How can you integrate AMP with Next.js?</b></summary>

Import the `withAmp` higher-order component and wrap your page:

```javascript
import { withAmp } from 'next/amp';

function MyPage() {
  return <div>AMP Page Content</div>;
}

export default withAmp(MyPage);
// or for hybrid: export default withAmp(MyPage, { hybrid: true });
```

**Modes:**
- **AMP-only**: Page served only as AMP
- **Hybrid**: Both AMP and non-AMP versions available

Note: AMP support is less commonly used now as Core Web Vitals can be achieved without AMP.
</details>

## I18n (Internationalization)

<details>
<summary><b>How to implement localization in React?</b></summary>

Libraries: react-i18next, react-intl. Setup: configure languages, create translation files (JSON), wrap app with provider, use translation hook/component.
</details>

<details>
<summary><b>How to use dynamic strings in a localization message in React?</b></summary>

Use interpolation. i18next: `t('greeting', { name: 'John' })` with `"greeting": "Hello {{name}}"`. react-intl: `<FormattedMessage values={{ name }}/>`.
</details>

<details>
<summary><b>How to do lazy loading of translations in React?</b></summary>

Load translations on demand per language/namespace. i18next has backend plugins for async loading. Load when user switches language or enters route.
</details>

<details>
<summary><b>Do you have experience and how it was implemented?</b></summary>

(Personal experience question - describe your project, challenges faced, library used, folder structure for translations, handling plurals and dates.)
</details>

## PWA & Service Workers

<details>
<summary><b>What is a progressive web app?</b></summary>

Web app with native-like features: installable, works offline, push notifications, fast loading. Uses: service workers, manifest file, HTTPS. Bridges gap between web and native apps.
</details>

<details>
<summary><b>What is a service worker?</b></summary>

JavaScript running in background, separate from main thread. Intercepts network requests. Enables: offline support, caching, push notifications, background sync. Lifecycle: install → activate → fetch.
</details>

<details>
<summary><b>What is an App Shell?</b></summary>

Minimal HTML/CSS/JS for basic UI structure. Cached by service worker. Loads instantly. Content fills in dynamically. Improves perceived performance.
</details>

<details>
<summary><b>What is Web App manifest?</b></summary>

JSON file (`manifest.json`) describing app. Contains: name, icons, theme color, start URL, display mode. Browser uses it for install prompt and home screen icon.
</details>

<details>
<summary><b>What are the requirements used to make the website installable as PWA?</b></summary>

Requirements: HTTPS, valid manifest file, service worker with fetch handler, icon (512x512), meets engagement heuristic (user interaction). Chrome shows install prompt.
</details>

## Google API

<details>
<summary><b>What Google API services did you use?</b></summary>

(Personal experience question - common ones: Maps API, Places API, Analytics, OAuth/Sign-in, Firebase, Cloud Storage, Sheets API, YouTube API.)
</details>

## React Style Guide

<details>
<summary><b>How do you keep state business logic separate from UI?</b></summary>

Custom hooks for logic, components for UI. Container/presentational pattern. Services layer for API calls. Components receive data via props, don't know where it comes from.
</details>

<details>
<summary><b>When should you avoid using State?</b></summary>

Avoid state for: derived data (calculate from existing state), constants, values not used in render, data that should come from props. Keep state minimal.
</details>

<details>
<summary><b>How do you use Object Destructuring for Props?</b></summary>

Destructure in function parameters or body:
```javascript
const Component = ({ name, age }) => <div>{name}, {age}</div>;
// or
const Component = (props) => { const { name, age } = props; };
```
</details>

## Programming Paradigms

<details>
<summary><b>Differentiate between imperative and declarative programming. And what kind is used in React?</b></summary>

- **Imperative**: Step-by-step how to do something (for loops, DOM manipulation)
- **Declarative**: Describe what you want (SQL, React JSX)

React is declarative - you describe UI based on state, React handles DOM updates.
</details>

## React Under the Hood

<details>
<summary><b>How does React work under the hood?</b></summary>

JSX compiles to `React.createElement()` calls. Creates virtual DOM tree. On state change: creates new virtual tree, diffs with old (reconciliation), generates minimal DOM updates. Fiber architecture enables: async rendering, prioritization, cancellation of updates.
</details>

## Server Components & Suspense

<details>
<summary><b>What are Server Components?</b></summary>

Components that render on the server, never sent to client. Benefits: zero bundle size, direct database/file access, automatic code splitting. Use for data fetching, heavy dependencies. Mark client components with 'use client' directive.
</details>

<details>
<summary><b>How do Server Components differ from SSR?</b></summary>

- **SSR**: Renders full page on server, then hydrates entire app on client. All code ships to client
- **Server Components**: Some components ONLY run on server, never hydrate. Reduced JS bundle, can use server-only APIs

Server Components are part of RSC architecture, complementary to SSR.
</details>

<details>
<summary><b>What are Suspense boundaries?</b></summary>

Suspense wraps components that might suspend (lazy loading, data fetching). Shows fallback while waiting:
```jsx
<Suspense fallback={<Loading />}>
  <LazyComponent />
</Suspense>
```
Enables streaming SSR, concurrent features. Can nest for granular loading states.
</details>

<details>
<summary><b>How do Error Boundaries work?</b></summary>

Class components that catch JS errors in child tree. Use `componentDidCatch` and `getDerivedStateFromError`. Show fallback UI instead of crashing app. Don't catch: event handlers, async code, SSR, errors in boundary itself.
</details>

<details>
<summary><b>Can Error Boundaries catch async errors?</b></summary>

Not directly. Errors in promises, setTimeout, event handlers aren't caught. Solutions: wrap async calls in try/catch and set error state, use error boundary with Suspense for data fetching errors in React 18+.
</details>

## React 19 Features

<details>
<summary><b>What are the new features in React 19?</b></summary>

React 19 improves async handling with:
- **Actions**: Simplified async state management with `useActionState`
- **`use` hook**: Read resources (promises, context) in render
- **Form handling**: `useFormStatus` for pending states
- **Server Components**: Better RSC support
- **Document metadata**: Native `<title>`, `<meta>` support
- **Asset loading**: Preloading APIs for resources

The goal is simpler and cleaner async code.
</details>

## Rendering Strategies

<details>
<summary><b>What are CSR, SSR, SSG, and ISR in Next.js? When to use each?</b></summary>

**CSR (Client-Side Rendering)**
Page renders in browser. JavaScript fetches data after page loads.

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
Use when: dashboards, user-specific content, SEO not important.

---

**SSR (Server-Side Rendering)**
Page renders on server for each request. Fresh data every time.

```jsx
// App Router - async component with no-store
async function Page() {
  const data = await fetch('https://api.example.com/data', {
    cache: 'no-store'
  });

  return <div>{data.title}</div>;
}
```
Use when: SEO important, data changes often, need fresh content.

---

**SSG (Static Site Generation)**
Page renders at build time. Same HTML for all users.

```jsx
// App Router - default caching behavior
async function Page() {
  const data = await fetch('https://api.example.com/data');
  // By default, fetch results are cached (SSG behavior)

  return <div>{data.title}</div>;
}
```
Use when: blogs, documentation, marketing pages, content rarely changes.

---

**ISR (Incremental Static Regeneration)**
Static page that rebuilds in background after specified time.

```jsx
async function Page() {
  const data = await fetch('https://api.example.com/data', {
    next: { revalidate: 60 } // Rebuild every 60 seconds
  });

  return <div>{data.title}</div>;
}
```
Use when: e-commerce products, news sites, need static speed but fresher data.

---

**Quick comparison:**
| Method | When renders | Data freshness | Performance |
|--------|-------------|----------------|-------------|
| CSR | Browser | Real-time | Fast initial, slow content |
| SSR | Every request | Fresh | Slower, good SEO |
| SSG | Build time | Stale | Fastest |
| ISR | Build + interval | Semi-fresh | Fast + updated |

</details>

## Code Splitting

<details>
<summary><b>What is Code Splitting?</b></summary>

Code splitting loads only the code that is needed. This improves performance and load time. Use `React.lazy()` + `Suspense` for components, dynamic `import()` for modules. Common in route-based splitting.
</details>

## React Patterns

<details>
<summary><b>What is the Container-Presenter Pattern?</b></summary>

Logic separate from UI. Container handles data/state, Presenter handles rendering. Benefits: minimum re-renders, maximum control, easier testing. Container passes data as props to Presenter.
</details>

<details>
<summary><b>What are Compound Components?</b></summary>

Pattern where parent component manages behavior of children. Like Radix UI or Headless UI. Children communicate through shared context. Example: `<Select><Select.Trigger/><Select.Options/></Select>`. Flexible API, encapsulated state.
</details>

<details>
<summary><b>What are Render Props (and their modern equivalent)?</b></summary>

Old: pass function as prop that returns UI. Modern: extract logic to custom hooks (`useXXX()`). Same idea - share behavior without sharing implementation. Hooks are cleaner and more composable.
</details>

<details>
<summary><b>What is State Colocation Pattern?</b></summary>

Keep state as close as possible to where it's used. Don't lift state higher than necessary. Benefits: fewer re-renders, easier to understand, better performance. Only lift when truly needed for sharing.
</details>

<details>
<summary><b>What is Event Propagation Pattern?</b></summary>

Pass callback events between deeply nested components instead of using context. Better for: performance (no context re-renders), explicit data flow, debugging. Use for component-specific events.
</details>

<details>
<summary><b>What is Context Module Pattern?</b></summary>

Make context modular to avoid excessive re-renders. Split context by concern, use selectors, memoize context values. Only re-render components that actually use changed data.
</details>

<details>
<summary><b>What is Smart Memoization Pattern?</b></summary>

Don't memoize everything - only "unstable" parts of the tree. Use `React.memo`, `useMemo`, `useCallback` strategically. Profile first to find actual bottlenecks. Over-memoization adds complexity without benefit.
</details>

<details>
<summary><b>What is Layout Shift Prevention Pattern?</b></summary>

Build UI to avoid jumps during hydration/loading. Reserve space for async content, use skeleton loaders, set explicit dimensions. Prevents CLS (Cumulative Layout Shift) issues.
</details>

<details>
<summary><b>What is Suspense + Resource Pattern?</b></summary>

Cached async resources with React Suspense (React 18+). Create resource that suspends while loading. Component reads resource, suspends if not ready. Base of modern data layers like React Query.
</details>

<details>
<summary><b>What is Error Boundary Pattern?</b></summary>

Catch errors at UI level without crashing entire app. Class component with `componentDidCatch` and `getDerivedStateFromError`. Show fallback UI on error. Use at route/feature boundaries.
</details>

<details>
<summary><b>What is State Machine Pattern?</b></summary>

Model complex UI states explicitly using state machines (XState or similar). Perfect for: forms, checkout flows, payments, wizards. States and transitions are explicit, impossible states are impossible.
</details>

<details>
<summary><b>What is Stale-While-Revalidate (SWR) Pattern?</b></summary>

Show cached data immediately, fetch fresh data in background. Used by Next.js App Router, SWR library, React Query. User sees content instantly, gets updates without blocking UI.
</details>

<details>
<summary><b>What is Adapter Pattern for integrations?</b></summary>

Single interface for different backends/SDKs/third-party data. Swap implementations without changing components. Example: same `useAuth()` hook works with Firebase, Auth0, or custom auth.
</details>

<details>
<summary><b>What is Selector Pattern in Zustand/Jotai/Recoil?</b></summary>

Split state into small selectors, components subscribe only to what they need. Minimal re-renders - component only updates when its specific slice changes. Example: `useStore(state => state.user.name)`.
</details>

<details>
<summary><b>What is View Transition Pattern?</b></summary>

Smooth animations between pages using the View Transitions API (2024+). Browser handles cross-document transitions. Enables native-like page animations without JS animation libraries.
</details>

<details>
<summary><b>What is Islands / Partial Hydration Pattern?</b></summary>

Hydrate only interactive parts ("islands") of the page. Rest stays as static HTML. Less JS on client, faster TTI. Used by Astro, Qwik. Trend for 2025 - ship less JavaScript.
</details>

<details>
<summary><b>What is Server Actions + Client Boundaries Pattern?</b></summary>

New Next.js architecture pattern. Server Actions handle mutations without API routes. Clear boundaries between server and client components. Simpler data flow, less boilerplate.
</details>

## Advanced Architecture

<details>
<summary><b>How would you build a component library architecture for scalable UI systems?</b></summary>

**Key principles:**

1. **Layered structure:**
   - Primitives (atoms): Button, Input, Text
   - Composites (molecules): SearchField, FormGroup
   - Features (organisms): DataTable, Modal

2. **Design tokens:**
```javascript
// tokens.js
export const tokens = {
  colors: { primary: '#007bff', error: '#dc3545' },
  spacing: { sm: '8px', md: '16px', lg: '24px' },
  typography: { body: '16px', heading: '24px' }
};
```

3. **Compound components for flexibility:**
```javascript
<Card>
  <Card.Header>Title</Card.Header>
  <Card.Body>Content</Card.Body>
  <Card.Footer>Actions</Card.Footer>
</Card>
```

4. **Polymorphic `as` prop:**
```javascript
<Button as="a" href="/link">Link Button</Button>
```

5. **Consistent API patterns:**
   - Controlled/uncontrolled support
   - Forwarded refs
   - Spread props to root element
   - Consistent naming (onX for events, isX for booleans)

6. **Documentation with Storybook + automated testing**
</details>

<details>
<summary><b>Explain the reconciliation and diffing algorithm in depth</b></summary>

**React's reconciliation** compares old and new virtual DOM trees to minimize actual DOM updates.

**Key heuristics:**

1. **Different element types = full rebuild:**
```jsx
// Old: <div><Counter /></div>
// New: <span><Counter /></span>
// Counter is completely destroyed and remounted
```

2. **Same element type = update attributes only:**
```jsx
// Old: <div className="old" />
// New: <div className="new" />
// Only className attribute is updated
```

3. **Keys for list identity:**
```jsx
// Without keys: React matches by index (causes issues with reordering)
// With keys: React matches elements by key (preserves state correctly)
{items.map(item => <Item key={item.id} {...item} />)}
```

**Fiber architecture (React 16+):**
- Work is broken into units (fibers)
- Rendering can be paused, resumed, or aborted
- Priority levels for updates (user interactions > data fetching)
- Concurrent features: Suspense, transitions

**Performance implications:**
- Avoid changing element types unnecessarily
- Use stable keys (not array index for dynamic lists)
- Lift state up when siblings share state
- Use React.memo for expensive pure components
</details>

<details>
<summary><b>Optimize rendering large lists — approaches other than virtualization</b></summary>

1. **Pagination / Infinite scroll:**
```javascript
const [page, setPage] = useState(1);
const items = allItems.slice(0, page * PAGE_SIZE);
```

2. **Debounced rendering:**
```javascript
// Render in batches using setTimeout
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

3. **Memoization at item level:**
```javascript
const MemoizedItem = React.memo(Item, (prev, next) =>
  prev.id === next.id && prev.updatedAt === next.updatedAt
);
```

4. **Deferred rendering with `useDeferredValue`:**
```javascript
const deferredList = useDeferredValue(list);
// Shows stale data during updates, preventing blocking
```

5. **Web Workers for heavy processing:**
```javascript
// Process/filter data off main thread
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
<summary><b>Design a custom hook for API polling with backoff</b></summary>

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
      // Reset interval on success
      currentInterval.current = interval;
    } catch (err) {
      setError(err);
      // Increase interval on failure (exponential backoff)
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

// Usage
const { data, error, stop } = usePolling(
  () => fetch('/api/status').then(r => r.json()),
  { interval: 3000 }
);
```
</details>

<details>
<summary><b>How do you solve stale closures in async React code?</b></summary>

**Problem:** Closures capture variable values at creation time, leading to stale data in async callbacks.

```javascript
// Problem
function Counter() {
  const [count, setCount] = useState(0);

  const handleClick = () => {
    setTimeout(() => {
      console.log(count); // Always logs initial value!
    }, 3000);
  };
}
```

**Solutions:**

1. **Use refs for current values:**
```javascript
const countRef = useRef(count);
useEffect(() => { countRef.current = count; }, [count]);

const handleClick = () => {
  setTimeout(() => {
    console.log(countRef.current); // Always current
  }, 3000);
};
```

2. **Functional updates for setState:**
```javascript
const handleClick = () => {
  setTimeout(() => {
    setCount(prevCount => prevCount + 1); // Uses latest value
  }, 3000);
};
```

3. **useCallback with proper dependencies:**
```javascript
const handleClick = useCallback(() => {
  // count is fresh here due to dependency
  console.log(count);
}, [count]);
```

4. **Use useEvent (React 18+) or custom hook:**
```javascript
function useEvent(handler) {
  const handlerRef = useRef(handler);
  useLayoutEffect(() => { handlerRef.current = handler; });
  return useCallback((...args) => handlerRef.current(...args), []);
}
```
</details>

<details>
<summary><b>How do you isolate global state updates from re-rendering deep child components?</b></summary>

1. **Selector pattern (Zustand/Redux):**
```javascript
// Only re-renders when user.name changes
const userName = useStore(state => state.user.name);
```

2. **Split context by concern:**
```javascript
// Bad: single context for everything
const AppContext = createContext({ user, theme, settings });

// Good: separate contexts
const UserContext = createContext(null);
const ThemeContext = createContext(null);
```

3. **Memoize context values:**
```javascript
const value = useMemo(() => ({ user, updateUser }), [user]);
return <UserContext.Provider value={value}>{children}</UserContext.Provider>;
```

4. **Component composition (extracting children):**
```javascript
// Instead of this (re-renders children on state change):
function Parent() {
  const [state, setState] = useState();
  return <div><ExpensiveChild /></div>;
}

// Do this (children don't re-render):
function Parent({ children }) {
  const [state, setState] = useState();
  return <div>{children}</div>;
}
<Parent><ExpensiveChild /></Parent>
```

5. **React.memo with custom comparison:**
```javascript
const DeepChild = React.memo(Component, (prev, next) => {
  return prev.relevantProp === next.relevantProp;
});
```
</details>

## Coding Challenges

<details>
<summary><b>Build a Grid Light Box with LIFO deactivation</b></summary>

Build a grid of clickable lights where clicking a light activates it, and clicking another light deactivates previously activated lights in reverse order (LIFO - Last In First Out).

**Requirements:**
- Grid of N x M cells
- Click to activate light
- Clicking already active light deactivates it
- Lights deactivate in reverse order of activation

```javascript
function GridLightBox({ rows = 3, cols = 3 }) {
  const [activeLights, setActiveLights] = useState([]);

  const handleLightClick = useCallback((id) => {
    setActiveLights(prev => {
      if (prev.includes(id)) {
        // Remove if already active
        return prev.filter(light => light !== id);
      }
      // Add to activation stack
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
        Deactivate Last
      </button>
    </div>
  );
}
```

**What's being tested:**
- State management with arrays (tracking activation order)
- Correct use of hooks (useCallback, useMemo)
- LIFO stack implementation
- Handling edge cases (clicking same light twice)
- Performance considerations (avoiding unnecessary re-renders)

**Follow-up questions:**
- What if we need activation animation sequence?
- How to add a "deactivate all" feature with animation delay?
- How to persist state to localStorage?
</details>

<details>
<summary><b>Create a reusable table component with sorting, pagination, filter & virtual scroll</b></summary>

```javascript
function useTable({ data, columns, pageSize = 10 }) {
  const [sortConfig, setSortConfig] = useState({ key: null, direction: 'asc' });
  const [filter, setFilter] = useState('');
  const [page, setPage] = useState(0);

  // Filter
  const filtered = useMemo(() => {
    if (!filter) return data;
    return data.filter(row =>
      columns.some(col =>
        String(row[col.key]).toLowerCase().includes(filter.toLowerCase())
      )
    );
  }, [data, filter, columns]);

  // Sort
  const sorted = useMemo(() => {
    if (!sortConfig.key) return filtered;
    return [...filtered].sort((a, b) => {
      const aVal = a[sortConfig.key];
      const bVal = b[sortConfig.key];
      const direction = sortConfig.direction === 'asc' ? 1 : -1;
      return aVal < bVal ? -direction : aVal > bVal ? direction : 0;
    });
  }, [filtered, sortConfig]);

  // Paginate
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

// With virtualization using react-window
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
<summary><b>Implement drag-and-drop without using any external library</b></summary>

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
<summary><b>Build a dynamic theme switcher with CSS variables</b></summary>

```javascript
// Theme definitions
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

// Theme context and hook
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

// Usage in components
function ThemeToggle() {
  const { theme, toggle } = useTheme();
  return <button onClick={toggle}>{theme === 'light' ? '🌙' : '☀️'}</button>;
}
```

**CSS usage:**
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
<summary><b>Render 10k items efficiently with intersection observer + virtualization</b></summary>

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

// With Intersection Observer for lazy loading images
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
