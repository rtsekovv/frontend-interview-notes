# Architecture Interview Questions

## Module Design

<details>
<summary><b>How do you participate in creating module design and/or its components?</b></summary>

Analyze requirements, identify responsibilities and boundaries. Create component diagrams. Define interfaces between modules. Consider: single responsibility, low coupling, high cohesion. Review with team, iterate based on feedback.
</details>

<details>
<summary><b>Describe your experience in creating and proposing system/module design</b></summary>

(Personal experience question - describe: gathering requirements, creating diagrams, presenting to team, handling feedback, trade-offs considered, tools used like Miro, draw.io, documentation format.)
</details>

## Technical Documentation

<details>
<summary><b>How do you prepare technical documentation?</b></summary>

Include: architecture overview, component descriptions, data flow diagrams, API documentation, setup instructions, deployment guide. Use clear language, diagrams, code examples. Keep it updated. Tools: Confluence, Notion, README files, JSDoc.
</details>

## Performance & Security

<details>
<summary><b>How do you resolve performance and security issues?</b></summary>

Performance: profile to find bottlenecks, measure before/after, use monitoring tools. Common fixes: caching, lazy loading, database optimization. Security: follow OWASP guidelines, audit dependencies, input validation, secure authentication. Regular security reviews.
</details>

## Architectural Patterns

<details>
<summary><b>What is the Retry pattern and when to use it?</b></summary>

Automatically retry failed operations (network calls, database). Use for transient failures. Implement: max retries, exponential backoff, timeout limits. Don't use for: validation errors, permanent failures. Consider circuit breaker for repeated failures.
</details>

<details>
<summary><b>What is the Health Endpoint Monitoring pattern?</b></summary>

Expose endpoint (e.g., `/health`) that returns service status. Check: dependencies (database, external services), memory, disk. Used by: load balancers, orchestrators (Kubernetes), monitoring systems. Return 200 if healthy, 503 if not.
</details>

<details>
<summary><b>What architectural approaches do you know?</b></summary>

- **Monolith**: Single deployable unit, simpler, good for small apps
- **Microservices**: Independent services, scalable, complex
- **Serverless**: Functions as a service, no server management
- **Event-driven**: Components communicate via events
- **Layered**: Presentation → Business → Data layers
</details>

## Solution Design

<details>
<summary><b>How do you explain pros and cons of proposed solutions?</b></summary>

Structure: describe solution briefly, list pros (benefits, fits requirements), list cons (risks, complexity, cost). Compare with alternatives. Use visual aids. Be objective, acknowledge trade-offs. Let stakeholders make informed decision.
</details>

<details>
<summary><b>How do you provide several possible solutions for an engineering problem?</b></summary>

Analyze problem first. Research existing solutions. Propose 2-3 options with different trade-offs (e.g., simple vs. scalable, fast vs. cheap). For each: describe approach, effort estimate, pros/cons. Recommend one with justification.
</details>

<details>
<summary><b>How do you decide which solution is better and why?</b></summary>

Evaluate against criteria: meets requirements, team expertise, time/budget constraints, maintainability, scalability needs, technical debt. Use weighted scoring if needed. Consider long-term impact. Get team input.
</details>

## Design Patterns in Architecture

<details>
<summary><b>How do you describe design patterns and architecture used on a project?</b></summary>

Document: overall architecture style (monolith, microservices), folder structure, major patterns used (MVC, Repository, Factory), data flow, key design decisions and why. Include diagrams. Keep accessible to new team members.
</details>

## Domain-Driven Design (DDD)

<details>
<summary><b>What is DDD (Domain-Driven Design)?</b></summary>

Approach focusing on core business domain. Key concepts: Ubiquitous Language (shared vocabulary), Bounded Contexts (clear boundaries), Entities (identity), Value Objects (no identity), Aggregates (consistency boundary), Domain Events. Useful for complex business logic.
</details>

## Clean Code Principles (DRY, YAGNI, KISS)

<details>
<summary><b>What are DRY, YAGNI, and KISS principles?</b></summary>

**DRY - Don't Repeat Yourself**
- Avoid code duplication
- Extract repeated logic into reusable functions/components
- Anti-pattern: Copy-pasting similar code blocks

**YAGNI - You Aren't Gonna Need It**
- Don't implement functionality until it's actually needed
- Anti-pattern: Adding features "for the future", making universal solutions without requirements
- Why bad: Complicates code, slows development, increases bugs

**KISS - Keep It Simple, Stupid**
- Prefer simplest solution that works
- Simplicity > "cleverness"
- Code is read more often than written

| Principle | Protects Against |
|-----------|------------------|
| DRY | Duplication |
| YAGNI | Premature complexity |
| KISS | Over-architecture |

**Interview one-liner:** DRY, YAGNI, and KISS are fundamental clean code principles. DRY reduces duplication, YAGNI protects from premature implementation of unneeded features, and KISS keeps solutions simple and maintainable. The key is applying them pragmatically, not dogmatically.
</details>

## MVC (Model-View-Controller)

<details>
<summary><b>What is MVC pattern?</b></summary>

MVC is an architectural pattern that separates application into three responsibilities:
- **Model** - data and business logic, knows nothing about UI
- **View** - data display (UI)
- **Controller** - handles user actions, coordinates Model and View

**Data flow:** User → Controller → Model → View

**Why use MVC:**
- Separation of concerns (SoC)
- Improved testability
- Easier to maintain
- Good for large applications

**MVC in modern frontend:**
Classic MVC is rarely used directly in frontend today. View and Controller often intertwine, DOM itself is the "View".

| MVC | React |
|-----|-------|
| Model | State |
| View | JSX / Template |
| Controller | Component / Hooks |

Often called **MV*** rather than strict MVC.

**Pros:** Clear separation, reusability, good for server apps

**Cons:** Complex for UI-heavy apps, Controller can grow large, not ideal for highly interactive SPAs

**Interview one-liner:** MVC is an architectural pattern that separates Model, View, and Controller to isolate business logic from presentation and user actions, improving maintainability and testability.
</details>

## Clean, Hexagonal, and Onion Architecture

<details>
<summary><b>What is Clean/Hexagonal/Onion Architecture?</b></summary>

All three are variations of the same idea: **business logic should be independent from UI, frameworks, DB, and infrastructure**. They differ in terminology and visual model, but philosophy is the same.

---

**1. Clean Architecture (Robert C. Martin)**

Divides system into layers with strict dependency rule: **dependencies always point inward**, toward business logic.

Layers (inside → out):
1. **Entities** - business rules, domain models
2. **Use Cases** - business scenarios, application logic
3. **Interface Adapters** - controllers, presenters, gateways
4. **Frameworks & Drivers** - UI (React), API, DB, third-party libs

---

**2. Hexagonal Architecture (Ports & Adapters)**

Focuses on **system's interaction with the external world**. Application is in the center, everything else connects through **ports and adapters**.

- **Ports** - interfaces, contracts (what system expects)
- **Adapters** - implementations (API, UI, DB, WebSocket)

Flow: `UI/API/Tests → Adapter → Port → Application Core`

---

**3. Onion Architecture**

Visually emphasizes **layering and dependency inversion**. Deeper layer = more stable and independent.

Layers: Domain → Domain Services → Application Services → Infrastructure → UI

Rule: Outer layers depend on inner, inner know nothing about outer.

---

**Comparison:**

| Aspect | Clean | Hexagonal | Onion |
|--------|-------|-----------|-------|
| Focus | Business rules | External interaction | Layering |
| Terms | Use Cases | Ports / Adapters | Domain |
| Dependencies | Inward | Through ports | Inward |
| Distinction | Formalization | Flexibility | Visual model |

**Frontend examples:**
- Use cases → `placeBet()`
- Entities → `Bet`, `Odds`
- Port → `OddsProvider` interface
- Adapter → REST / SSE / WebSocket implementation
- UI (React) → just calls use cases

**Pros:** Testability, loose coupling, framework independence, ready for changes

**Cons:** Overengineering for small projects, more code and abstractions, requires mature team

**Interview one-liner:** Clean, Hexagonal, and Onion Architecture share the same goal: isolate business logic from UI and infrastructure with dependencies pointing inward. They differ in terminology but provide high testability, extensibility, and framework independence.
</details>

## Dependency Inversion vs Dependency Injection

<details>
<summary><b>What is the difference between Dependency Inversion (DIP) and Dependency Injection (DI)?</b></summary>

**Dependency Inversion Principle (DIP)** - SOLID principle:
- High-level modules should not depend on low-level modules
- Both should depend on abstractions
- Abstractions should not depend on details

**Dependency Injection (DI)** - Technique to implement DIP:
- Dependencies are passed in (injected) from outside, not created inside
- DI is a way to achieve Dependency Inversion

**Without DI (tight coupling):**
```javascript
class UserService {
  constructor() {
    this.api = new ApiService(); // Hard dependency
  }
}
```

**With DI (loose coupling):**
```javascript
class UserService {
  constructor(api) {
    this.api = api; // Dependency injected
  }
}
const userService = new UserService(new ApiService());
```

**DI in Frontend Frameworks:**
- **React**: Props, Context API
- **Angular**: Built-in DI container (`@Injectable()`)
- **Vue**: `provide` / `inject`

| Aspect | DIP | DI |
|--------|-----|-----|
| Type | Principle | Technique |
| Focus | How modules should depend | How to pass dependencies |
| Level | Architectural | Implementation |

**Interview one-liner:** DIP is the principle that modules should depend on abstractions; DI is the technique of passing dependencies from outside to achieve loose coupling and testability.
</details>

## Frontend System Design

<details>
<summary><b>Design an online code editor like StackBlitz (frontend system design)</b></summary>

**Core requirements:**
- File system with tree navigation
- Multi-file code editing with syntax highlighting
- Live preview/execution
- Real-time collaboration (optional)

**Architecture:**

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

**Key components:**

1. **Code Editor:**
   - Use Monaco Editor (VS Code engine) or CodeMirror
   - Features: syntax highlighting, autocomplete, multi-cursor

2. **Virtual File System:**
   - In-memory file tree with IndexedDB persistence
   - File operations: create, read, update, delete, rename
   - Watch for changes and trigger rebuilds

3. **Bundler/Transpiler:**
   - Option A: esbuild-wasm for browser-based bundling
   - Option B: WebContainer (StackBlitz technology) - Node.js in browser
   - Handle npm dependencies via esm.sh or Skypack CDN

4. **Preview Panel:**
   - Sandboxed iframe with srcdoc or blob URL
   - Hot Module Replacement for instant updates
   - Error boundary for runtime errors

**State management:**
```typescript
interface EditorState {
  files: Map<string, FileNode>;
  openTabs: string[];
  activeFile: string;
  unsavedChanges: Set<string>;
}

interface FileNode {
  name: string;
  type: 'file' | 'directory';
  content?: string;
  children?: FileNode[];
}
```

**Performance considerations:**
- Debounce compilation on keystroke
- Web Workers for heavy operations (parsing, bundling)
- Virtual scrolling for large files
- Lazy load editor features
</details>

<details>
<summary><b>Design a notification system with offline support</b></summary>

**Requirements:**
- Real-time push notifications
- Notification center with history
- Offline storage and sync
- Read/unread status across devices

**Architecture:**

```
┌──────────────────────────────────────────────────────┐
│                    Frontend                           │
├──────────────────────────────────────────────────────┤
│  Notification │  Service Worker  │  IndexedDB Cache  │
│  Center UI    │  (Push + Sync)   │  (Offline Store)  │
├──────────────────────────────────────────────────────┤
│              Notification Manager                     │
│  - Queue management                                   │
│  - Deduplication                                      │
│  - Priority handling                                  │
└──────────────────────────────────────────────────────┘
              │
              │ WebSocket / Server-Sent Events
              ▼
┌──────────────────────────────────────────────────────┐
│                    Backend                            │
│  Notification Service → Message Queue → Push Service │
└──────────────────────────────────────────────────────┘
```

**Implementation:**

```typescript
// Notification Manager
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
    // Store locally first (offline-first)
    await this.storeLocal(notification);
    // Update UI
    this.emit('notification', notification);
    // Show system notification if permitted
    if (notification.showPush) {
      this.showPushNotification(notification);
    }
  }

  async markAsRead(id: string) {
    // Update local state
    await this.updateLocal(id, { read: true, readAt: Date.now() });

    // Queue sync if offline
    if (!navigator.onLine) {
      this.pendingSync.push({ action: 'markRead', id });
      return;
    }

    // Sync with server
    await this.syncWithServer({ action: 'markRead', id });
  }

  private async syncPendingActions() {
    window.addEventListener('online', async () => {
      for (const action of this.pendingSync) {
        await this.syncWithServer(action);
      }
      this.pendingSync = [];
    });
  }
}
```

**Service Worker for Push:**
```javascript
// sw.js
self.addEventListener('push', (event) => {
  const data = event.data.json();
  event.waitUntil(
    self.registration.showNotification(data.title, {
      body: data.body,
      icon: '/icon.png',
      data: { url: data.url }
    })
  );
});

self.addEventListener('notificationclick', (event) => {
  event.notification.close();
  event.waitUntil(clients.openWindow(event.notification.data.url));
});
```

**Offline sync strategy:**
- Store all notifications in IndexedDB
- Track pending actions (read, dismiss)
- Background Sync API for deferred server sync
- Conflict resolution: last-write-wins with timestamps
</details>

<details>
<summary><b>Build a micro-frontend architecture for a large enterprise app</b></summary>

**When to use micro-frontends:**
- Multiple teams working on same product
- Need to deploy features independently
- Legacy modernization (gradual migration)
- Different tech stack requirements

**Integration approaches:**

1. **Build-time integration (Module Federation):**
```javascript
// webpack.config.js - Host app
new ModuleFederationPlugin({
  name: 'host',
  remotes: {
    dashboard: 'dashboard@http://localhost:3001/remoteEntry.js',
    settings: 'settings@http://localhost:3002/remoteEntry.js',
  },
  shared: ['react', 'react-dom'],
});

// Usage in host
const Dashboard = React.lazy(() => import('dashboard/App'));
```

2. **Runtime integration (Single-SPA):**
```javascript
// root-config.js
registerApplication({
  name: '@org/dashboard',
  app: () => System.import('@org/dashboard'),
  activeWhen: ['/dashboard'],
});

start();
```

3. **iFrame integration:**
```html
<!-- Simple but limited -->
<iframe src="https://dashboard.example.com" />
```

**Shared concerns:**

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

**Communication between MFEs:**
```typescript
// Custom events
window.dispatchEvent(new CustomEvent('user:updated', { detail: user }));
window.addEventListener('user:updated', (e) => handleUserUpdate(e.detail));

// Shared state (with caution)
const sharedStore = {
  user: null,
  subscribe: (callback) => { /* ... */ }
};
```

**Challenges and solutions:**
- **Consistent styling**: Shared design system as npm package
- **Shared state**: Event bus or shared store (Redux with namespacing)
- **Routing**: Centralized router in shell, MFEs handle sub-routes
- **Performance**: Shared dependencies, lazy loading MFEs
</details>

<details>
<summary><b>How to secure frontend routes + tokens in a real app?</b></summary>

**Route protection:**
```typescript
// Protected Route component
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

// Usage
<Route path="/admin" element={
  <ProtectedRoute requiredRoles={['admin']}>
    <AdminDashboard />
  </ProtectedRoute>
} />
```

**Token management:**

```typescript
// Secure token storage
class TokenManager {
  // Access token - short-lived, stored in memory
  private accessToken: string | null = null;

  // Refresh token - httpOnly cookie (set by server)
  // Cannot be accessed by JavaScript = XSS safe

  setAccessToken(token: string) {
    this.accessToken = token;
  }

  getAccessToken() {
    return this.accessToken;
  }

  async refreshAccessToken() {
    // Cookie is automatically sent
    const response = await fetch('/api/auth/refresh', {
      method: 'POST',
      credentials: 'include', // Include cookies
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

**API request interceptor:**
```typescript
// Axios interceptor for token refresh
api.interceptors.response.use(
  (response) => response,
  async (error) => {
    const originalRequest = error.config;

    if (error.response?.status === 401 && !originalRequest._retry) {
      originalRequest._retry = true;

      try {
        const newToken = await tokenManager.refreshAccessToken();
        originalRequest.headers.Authorization = `Bearer ${newToken}`;
        return api(originalRequest);
      } catch (refreshError) {
        // Redirect to login
        window.location.href = '/login';
        return Promise.reject(refreshError);
      }
    }

    return Promise.reject(error);
  }
);
```

**Security best practices:**
1. **Never store tokens in localStorage** - vulnerable to XSS
2. **Use httpOnly cookies for refresh tokens** - inaccessible to JS
3. **Short-lived access tokens** (5-15 min)
4. **Implement CSRF protection** for cookie-based auth
5. **Validate on server** - frontend checks are for UX only
</details>

<details>
<summary><b>Design a real-time dashboard with charts & streaming data</b></summary>

**Requirements:**
- Real-time data updates (1-5 second intervals)
- Multiple chart types (line, bar, pie)
- Performant with thousands of data points
- Handle connection issues gracefully

**Architecture:**

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

**Real-time data handling:**

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
      // Reconnect with exponential backoff
      setTimeout(() => this.connect(), this.getBackoffDelay());
    };
  }

  private processData(data: StreamData) {
    const { metric, value, timestamp } = data;

    // Update buffer
    if (!this.buffer.has(metric)) {
      this.buffer.set(metric, []);
    }

    const metricBuffer = this.buffer.get(metric)!;
    metricBuffer.push({ value, timestamp });

    // Trim buffer
    if (metricBuffer.length > this.maxBufferSize) {
      metricBuffer.shift();
    }

    // Notify subscribers (throttled)
    this.notifySubscribers(metric);
  }

  subscribe(metric: string, callback: Callback) {
    if (!this.subscribers.has(metric)) {
      this.subscribers.set(metric, new Set());
    }
    this.subscribers.get(metric)!.add(callback);

    // Return unsubscribe function
    return () => this.subscribers.get(metric)?.delete(callback);
  }
}
```

**Chart optimization:**

```typescript
// React component with optimized rendering
function RealtimeChart({ metricId }) {
  const chartRef = useRef<Chart>();
  const dataManager = useDashboardData();

  useEffect(() => {
    // Initialize chart
    chartRef.current = new Chart(canvasRef.current, {
      type: 'line',
      options: {
        animation: false, // Disable for performance
        parsing: false,   // Pre-parsed data
        normalized: true,
        spanGaps: true,
      }
    });

    // Subscribe to updates
    const unsubscribe = dataManager.subscribe(metricId, (data) => {
      // Update chart data directly (no React re-render)
      chartRef.current.data.datasets[0].data = data;
      chartRef.current.update('none'); // No animation
    });

    return () => {
      unsubscribe();
      chartRef.current?.destroy();
    };
  }, [metricId]);

  return <canvas ref={canvasRef} />;
}
```

**Performance techniques:**
- Use canvas-based charts (Chart.js, ECharts)
- Batch DOM updates with requestAnimationFrame
- Downsample data for display (keep full data for zooming)
- Web Workers for data processing
- Throttle/debounce UI updates (max 30-60 fps)
</details>

## Scalability & Code Quality

<details>
<summary><b>How would you structure a large React application?</b></summary>

Feature-based structure (not by file type):
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
Each feature is self-contained. Shared folder for common utilities. Clear import rules between features.
</details>

<details>
<summary><b>Where do you put business logic in a React app?</b></summary>

- **Custom hooks**: For reusable stateful logic
- **Services/utils**: For pure business logic without React dependencies
- **State managers**: For complex state transformations
- **NOT in components**: Components should be thin, focused on rendering

Keep components dumb, logic in dedicated layers. Easier to test and maintain.
</details>

<details>
<summary><b>How do you handle cross-cutting concerns?</b></summary>

Cross-cutting: logging, auth, error handling, analytics. Solutions:
- **Higher-Order Components**: Wrap components with shared logic
- **Custom hooks**: Share logic across components
- **Context**: Provide global functionality
- **Middleware**: For state management actions
- **Aspect-oriented patterns**: Decorators, interceptors
</details>

<details>
<summary><b>How do you handle technical debt?</b></summary>

1. **Track it**: Document in backlog with impact/effort
2. **Allocate time**: 10-20% of sprint for debt reduction
3. **Prioritize**: Fix high-impact, low-effort items first
4. **Prevent**: Code reviews, standards, automated checks
5. **Refactor incrementally**: Don't wait for big rewrites

Balance new features with maintenance. Make debt visible to stakeholders.
</details>

<details>
<summary><b>How do you implement feature flags?</b></summary>

Feature flags control feature availability without code changes:
```javascript
if (featureFlags.newCheckout) {
  return <NewCheckout />;
}
return <OldCheckout />;
```
Use for: gradual rollouts, A/B testing, quick rollbacks, trunk-based development.

Tools: LaunchDarkly, Unleash, custom solution with config.
</details>

<details>
<summary><b>What coding standards do you follow?</b></summary>

- **Linting**: ESLint with team-agreed rules
- **Formatting**: Prettier for consistency
- **Naming**: Clear, descriptive names (no abbreviations)
- **File structure**: Consistent organization
- **TypeScript**: Strict mode, avoid `any`
- **Git**: Conventional commits, meaningful messages

Automate with pre-commit hooks. Document in team guidelines.
</details>

<details>
<summary><b>What makes code readable?</b></summary>

- **Clear naming**: Variables and functions describe their purpose
- **Small functions**: Single responsibility, 10-20 lines ideal
- **Consistent style**: Same patterns throughout codebase
- **Meaningful abstractions**: Right level of abstraction
- **Comments when needed**: Explain "why", not "what"
- **Tests as documentation**: Show how code should be used

Code is read 10x more than written. Optimize for reading.
</details>
