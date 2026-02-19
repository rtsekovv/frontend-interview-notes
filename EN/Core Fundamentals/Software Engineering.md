# Software Engineering Interview Questions

## Debugging

<details>
<summary><b>How do you debug code? What tools do you use?</b></summary>

I use browser DevTools (Chrome/Firefox) for frontend - breakpoints, console.log, network tab, performance profiler. For Node.js - built-in debugger or VS Code debugger. Also use React DevTools, Redux DevTools for state inspection. Start by reproducing the bug, then narrow down the problem area step by step.
</details>

## Clean Code (SOLID, DRY, YAGNI, KISS)

<details>
<summary><b>What is SOLID? Explain each principle</b></summary>

- **S** - Single Responsibility: Class should have only one reason to change
- **O** - Open/Closed: Open for extension, closed for modification
- **L** - Liskov Substitution: Child classes should be replaceable for parent classes
- **I** - Interface Segregation: Many small interfaces better than one big interface
- **D** - Dependency Inversion: Depend on abstractions, not concrete implementations
</details>

<details>
<summary><b>What is DRY (Don't Repeat Yourself)?</b></summary>

Avoid code duplication. If you write same logic twice, extract it to a function or module. But don't over-abstract - some duplication is okay if contexts are different.
</details>

<details>
<summary><b>What is YAGNI (You Aren't Gonna Need It)?</b></summary>

Don't implement features until you actually need them. Avoid premature optimization and building functionality "just in case". Focus on current requirements.
</details>

<details>
<summary><b>What is KISS (Keep It Simple, Stupid)?</b></summary>

Write simple, readable code. Avoid over-engineering. Simple solution that works is better than complex "clever" solution. Future you (or teammates) should easily understand the code.
</details>

## OOP

<details>
<summary><b>Explain the basics of OOP (Object-Oriented Programming)</b></summary>

Four main pillars:
- **Encapsulation**: Bundle data and methods together, hide internal details
- **Abstraction**: Show only necessary details, hide complexity
- **Inheritance**: Child class inherits properties/methods from parent
- **Polymorphism**: Same interface, different implementations (method overriding)
</details>

## MVC

<details>
<summary><b>What is MVC architecture?</b></summary>

Model-View-Controller pattern separates application into three parts:
- **Model**: Data and business logic
- **View**: UI/presentation layer (what user sees)
- **Controller**: Handles user input, updates Model, selects View

Benefits: separation of concerns, easier testing, parallel development.
</details>

## CI/CD & Static Code Analyzers

<details>
<summary><b>How do you set up CI/CD?</b></summary>

Use tools like GitHub Actions, GitLab CI, Jenkins. Setup includes: automated tests on each PR, linting checks, build process, deployment to staging/production. Example flow: push code → run tests → build → deploy to staging → manual approval → deploy to production.
</details>

<details>
<summary><b>What static code analyzers do you use?</b></summary>

ESLint for JavaScript/TypeScript (catches errors, enforces style), Prettier for formatting, SonarQube for deeper analysis (security, code smells). TypeScript compiler itself is also a static analyzer.
</details>

## Production Support & Monitoring

<details>
<summary><b>How do you handle production support and monitoring?</b></summary>

Use monitoring tools: Sentry for error tracking, DataDog/New Relic for performance monitoring, CloudWatch for AWS logs. Set up alerts for errors and performance issues. Implement logging at different levels (info, warn, error). Have on-call rotation and incident response procedures.
</details>

## Estimation

<details>
<summary><b>How do you estimate tasks?</b></summary>

Break task into smaller parts, consider: development time, testing, code review, potential blockers. Use story points or hours. Account for complexity and unknowns. Compare with similar past tasks. Add buffer for unexpected issues (usually 20-30%). Discuss with team if unsure.
</details>

## Architecture (Clean, Hexagonal, Onion)

<details>
<summary><b>What is Clean Architecture?</b></summary>

Layers separated by dependency rule - inner layers don't know about outer layers. Entities (core business) → Use Cases → Controllers/Presenters → External (DB, UI). Makes code testable and framework-independent.
</details>

<details>
<summary><b>What is Hexagonal Architecture?</b></summary>

Also called "Ports and Adapters". Core business logic in center, communicates with outside world through ports (interfaces) and adapters (implementations). Easy to swap databases, UIs, external services without changing core logic.
</details>

<details>
<summary><b>What is Onion Architecture?</b></summary>

Similar to Clean Architecture. Layers like onion - Domain Model at center, then Domain Services, then Application Services, then Infrastructure. Dependencies point inward. Core doesn't depend on external concerns.
</details>

## Application Performance

<details>
<summary><b>What application performance models do you know?</b></summary>

Key metrics: Time to First Byte (TTFB), First Contentful Paint (FCP), Largest Contentful Paint (LCP), Time to Interactive (TTI), Cumulative Layout Shift (CLS). Models: RAIL (Response, Animation, Idle, Load) by Google - response <100ms, animations 60fps, idle work <50ms, load <1s.
</details>

<details>
<summary><b>How do you optimize application performance?</b></summary>

Frontend: code splitting, lazy loading, image optimization, caching, minification, tree shaking, CDN. Reduce bundle size. Avoid unnecessary re-renders (React.memo, useMemo). Backend: database indexing, query optimization, caching (Redis), pagination. Profile first, then optimize bottlenecks.
</details>

## Test Pyramid

<details>
<summary><b>Explain the Test Pyramid and how you apply it in projects</b></summary>

Pyramid shape - most tests at bottom, fewer at top:
- **Unit tests** (bottom): Many, fast, test single functions/components
- **Integration tests** (middle): Test how modules work together
- **E2E tests** (top): Few, slow, test full user flows

Apply by writing many unit tests, some integration tests, few E2E tests for critical paths. Fast feedback loop is key.
</details>

## React Experimental Features

<details>
<summary><b>What is the Activity component in React?</b></summary>

`<Activity>` is an experimental component for priority-based lifecycle management. It allows you to hide/show parts of UI while keeping their state preserved.

**Key features:**
- `mode="hidden"` - component is hidden but state is preserved
- `mode="visible"` - component is shown normally
- Lower priority for hidden components - React can defer their updates

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

**Use cases:**
- Tab navigation without losing state
- Offscreen prerendering
- Keeping form state when switching views

Note: This is experimental and may change before stable release.
</details>

<details>
<summary><b>What is useEffectEvent hook and what problem does it solve?</b></summary>

`useEffectEvent` solves the "stale closure" problem in useEffect dependency arrays. It creates a stable function that always has access to latest values without being a dependency.

**Problem it solves:**
```jsx
// Problem: need to add onTick to deps, but it changes every render
function Timer({ onTick, interval }) {
  useEffect(() => {
    const id = setInterval(() => onTick(), interval);
    return () => clearInterval(id);
  }, [onTick, interval]); // onTick causes unnecessary restarts
}
```

**Solution with useEffectEvent:**
```jsx
import { useEffectEvent } from 'react';

function Timer({ onTick, interval }) {
  const tick = useEffectEvent(() => {
    onTick(); // Always has latest onTick
  });

  useEffect(() => {
    const id = setInterval(tick, interval);
    return () => clearInterval(id);
  }, [interval]); // tick is stable, not needed in deps
}
```

**Key points:**
- Function created by useEffectEvent is stable (same reference)
- Always reads latest props/state when called
- Should not be called during render
- Only use inside useEffect

Note: Currently experimental, use with caution.
</details>

<details>
<summary><b>What is cacheSignal API in React Server Components?</b></summary>

`cacheSignal` is an experimental API for controlling cache invalidation in React Server Components. It provides a signal to abort cached operations when cache is cleared.

**Basic usage:**
```jsx
import { unstable_cacheSignal as cacheSignal } from 'react';
import { cache } from 'react';

const fetchData = cache(async (id) => {
  const signal = cacheSignal();

  const response = await fetch(`/api/data/${id}`, {
    signal // Abort if cache is invalidated
  });

  return response.json();
});
```

**Why it matters:**
- Prevents stale requests from completing after cache clear
- Saves resources by aborting unnecessary fetches
- Works with any AbortSignal-compatible API

**Use cases:**
- Long-running server data fetches
- Canceling outdated requests on navigation
- Resource cleanup when cache invalidates

Note: This is experimental and prefixed with `unstable_`. API may change.
</details>
