# General Development Skills Interview Questions

## Git & Git Flow

<details>
<summary><b>Explain Git Flow branching model</b></summary>

Branches: `main` (production), `develop` (integration), `feature/*` (new features), `release/*` (prepare release), `hotfix/*` (urgent fixes). Flow: create feature from develop → merge to develop → create release → merge to main and develop. Tags for versions.
</details>

## Environments

<details>
<summary><b>What are different environments (dev, staging, production)?</b></summary>

- **Development**: Local machine, frequent changes, debug mode
- **Staging**: Production-like, for QA testing, safe to break
- **Production**: Live users, stable, monitored, no debugging

Each has own config, database, API keys. CI/CD deploys to each.
</details>

## HTTP/HTTPS

<details>
<summary><b>What is the difference between HTTP and HTTPS?</b></summary>

- **HTTP**: Unencrypted, data visible to attackers, port 80
- **HTTPS**: Encrypted with TLS/SSL, secure, port 443, requires certificate

Always use HTTPS for production. Required for: passwords, payments, cookies, SEO benefits.
</details>

## Bash & Terminal

<details>
<summary><b>What are basic Bash commands you use daily?</b></summary>

Navigation: `cd`, `ls`, `pwd`. Files: `cat`, `mkdir`, `rm`, `cp`, `mv`. Git: `git status/add/commit/push/pull`. npm: `npm install/run/test`. Search: `grep`, `find`. Others: `curl`, `chmod`, `ps`, `kill`.
</details>

## Docker

<details>
<summary><b>What is Docker? Explain image, container, volume, registry</b></summary>

- **Docker**: Platform for containerized applications
- **Image**: Blueprint/template, read-only, contains app and dependencies
- **Container**: Running instance of image, isolated environment
- **Volume**: Persistent storage, survives container restart
- **Registry**: Image repository (Docker Hub, ECR)
</details>

<details>
<summary><b>How do you write a Dockerfile?</b></summary>

```dockerfile
FROM node:18-alpine       # Base image
WORKDIR /app              # Set working directory
COPY package*.json ./     # Copy dependency files
RUN npm install           # Install dependencies
COPY . .                  # Copy source code
EXPOSE 3000               # Document port
CMD ["npm", "start"]      # Run command
```
</details>

## JWT

<details>
<summary><b>What is JWT and how does it work?</b></summary>

JSON Web Token - compact, URL-safe token for authentication. Three parts: Header (algorithm), Payload (claims/data), Signature (verify integrity). Server creates token on login, client sends in Authorization header. Server verifies signature, no session storage needed.
</details>

## Hosting & Domains

<details>
<summary><b>How do you set up hosting and domains?</b></summary>

Domain: buy from registrar (Namecheap, GoDaddy). Hosting: choose provider (Vercel, AWS, DigitalOcean). Configure DNS: A record (IP) or CNAME (domain). Setup SSL certificate (Let's Encrypt free). Configure web server (nginx) or use platform defaults.
</details>

## CI/CD

<details>
<summary><b>How do you set up CI/CD pipelines?</b></summary>

Tools: GitHub Actions, GitLab CI, Jenkins. Setup: create config file (`.github/workflows/`). Steps: install deps → lint → test → build → deploy. Triggers: push, PR, schedule. Secrets for API keys. Deploy to staging on merge, production on release.
</details>

## Code Quality (Linters & Formatters)

<details>
<summary><b>What code linters and formatters do you use?</b></summary>

- **ESLint**: Catches errors, enforces rules
- **Prettier**: Auto-formats code
- **TypeScript**: Type checking
- **Stylelint**: CSS linting

Setup: config files, IDE integration, pre-commit hooks (husky + lint-staged).
</details>

## Dependency Inversion & Injection

<details>
<summary><b>What is Dependency Inversion principle?</b></summary>

High-level modules shouldn't depend on low-level modules. Both should depend on abstractions. Example: service depends on interface, not concrete database class. Benefits: easier testing, swappable implementations.
</details>

<details>
<summary><b>What is Dependency Injection and why is it useful?</b></summary>

Pass dependencies to component instead of creating inside. Types: constructor injection, setter injection, interface injection. Benefits: loose coupling, testable (inject mocks), flexible. Frameworks: Angular has built-in DI.
</details>

## Infrastructure

<details>
<summary><b>How do you configure project infrastructure from scratch?</b></summary>

Steps: choose hosting (cloud/VPS), setup server/container, configure web server, setup database, configure domains/SSL, setup CI/CD, configure monitoring/logging, environment variables, backup strategy. Document everything.
</details>

## Data Structures

<details>
<summary><b>What data structures do you commonly use?</b></summary>

- **Array**: Ordered list, fast index access
- **Object/Map**: Key-value pairs, fast lookup
- **Set**: Unique values, fast membership check
- **Stack**: LIFO (undo functionality)
- **Queue**: FIFO (task processing)
- **Tree**: DOM, file systems, hierarchical data
</details>

## Algorithms

<details>
<summary><b>What algorithms are important for frontend development?</b></summary>

- **Searching**: Binary search (sorted data)
- **Sorting**: Understanding built-in sort
- **Debounce/Throttle**: Rate limiting
- **Memoization**: Caching results
- **Tree traversal**: DOM manipulation
- **Diffing**: Virtual DOM (React's algorithm)
</details>

## Debugging & Performance

<details>
<summary><b>App takes 8 seconds to load — how to analyze & fix?</b></summary>

**Diagnostic approach:**

1. **Measure first** (Lighthouse, WebPageTest, Chrome DevTools):
```
Performance tab → Record page load → Analyze waterfall
```

2. **Common culprits and solutions:**

**Network issues:**
- Large bundle sizes → Code splitting, lazy loading
- Too many requests → Bundle, sprite sheets, HTTP/2
- Slow TTFB → CDN, server optimization, caching
- No compression → Enable gzip/brotli

**JavaScript issues:**
```javascript
// Check bundle analysis
npx webpack-bundle-analyzer stats.json

// Code splitting
const HeavyComponent = lazy(() => import('./Heavy'));
```

**Render blocking:**
```html
<!-- Move scripts to bottom or use defer -->
<script src="app.js" defer></script>

<!-- Critical CSS inline, rest async -->
<style>/* critical */</style>
<link rel="preload" href="styles.css" as="style" onload="this.rel='stylesheet'">
```

**Large assets:**
```html
<!-- Responsive images -->
<img srcset="small.jpg 480w, large.jpg 800w" sizes="100vw" />

<!-- Lazy load below-fold images -->
<img loading="lazy" src="below-fold.jpg" />
```

**Checklist:**
- [ ] Analyze bundle size (target: <200KB gzipped for initial)
- [ ] Check for render-blocking resources
- [ ] Verify caching headers
- [ ] Test on throttled connection (3G)
- [ ] Check third-party script impact
- [ ] Review Web Vitals (LCP, FID, CLS)
</details>

<details>
<summary><b>Random logout issue after token refresh — how to debug?</b></summary>

**Investigation steps:**

1. **Add comprehensive logging:**
```typescript
class AuthLogger {
  log(event: string, data?: any) {
    console.log(`[Auth ${new Date().toISOString()}] ${event}`, data);
    // Also send to monitoring service
    analytics.track('auth_event', { event, ...data });
  }
}

// In token refresh flow
authLogger.log('refresh_started', { tokenAge });
try {
  const newToken = await refreshToken();
  authLogger.log('refresh_success', { newTokenExpiry });
} catch (error) {
  authLogger.log('refresh_failed', { error: error.message, status: error.status });
}
```

2. **Common causes:**

**Race conditions:**
```typescript
// Problem: Multiple tabs refreshing simultaneously
// Solution: Use locks
const refreshLock = new Lock('token_refresh');

async function refreshTokenSafe() {
  if (await refreshLock.acquire()) {
    try {
      return await refreshToken();
    } finally {
      refreshLock.release();
    }
  }
  // Wait for other tab's refresh
  return waitForNewToken();
}
```

**Timing issues:**
```typescript
// Problem: Token expires during refresh request
// Solution: Refresh before expiry
const REFRESH_BUFFER = 60 * 1000; // 1 minute before expiry

function shouldRefresh(token) {
  const expiry = decodeToken(token).exp * 1000;
  return Date.now() > expiry - REFRESH_BUFFER;
}
```

**Cookie issues:**
- Check SameSite attribute for cross-origin
- Verify Secure flag for HTTPS
- Check domain/path settings

**Network issues:**
```typescript
// Handle network failures gracefully
async function refreshWithRetry(retries = 3) {
  for (let i = 0; i < retries; i++) {
    try {
      return await refreshToken();
    } catch (e) {
      if (i === retries - 1) throw e;
      await delay(1000 * Math.pow(2, i)); // Exponential backoff
    }
  }
}
```
</details>

<details>
<summary><b>UI freezing during scroll — how to profile & solve?</b></summary>

**Profiling:**
```
Chrome DevTools → Performance tab → Record while scrolling
Look for: Long tasks (>50ms), Layout thrashing, Excessive paints
```

**Common causes and solutions:**

1. **Too many DOM nodes:**
```javascript
// Problem: Rendering 10000 list items
// Solution: Virtualization
import { FixedSizeList } from 'react-window';

<FixedSizeList height={600} itemCount={10000} itemSize={50}>
  {({ index, style }) => <Row style={style} data={items[index]} />}
</FixedSizeList>
```

2. **Layout thrashing:**
```javascript
// Bad: Forces layout on each iteration
items.forEach(item => {
  const height = element.offsetHeight; // Read (forces layout)
  element.style.height = height + 10 + 'px'; // Write
});

// Good: Batch reads and writes
const heights = items.map(() => element.offsetHeight); // All reads
items.forEach((item, i) => {
  element.style.height = heights[i] + 10 + 'px'; // All writes
});
```

3. **Expensive scroll handlers:**
```javascript
// Bad
window.addEventListener('scroll', () => {
  expensiveOperation();
});

// Good: Throttle + RAF
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

4. **CSS optimizations:**
```css
/* Use will-change for animated elements */
.animated { will-change: transform; }

/* Use transform instead of top/left */
.moving { transform: translateY(100px); }

/* Use CSS containment */
.list-item { contain: layout style paint; }
```

5. **Image loading:**
```html
<!-- Use loading="lazy" for off-screen images -->
<img loading="lazy" src="below-fold.jpg" />

<!-- Use aspect-ratio to prevent layout shifts -->
<img style="aspect-ratio: 16/9" src="image.jpg" />
```
</details>

<details>
<summary><b>Memory leak due to subscriptions — how to detect & prevent?</b></summary>

**Detection:**
```
Chrome DevTools → Memory tab → Take heap snapshot
→ Do operations → Take another snapshot
→ Compare: Look for growing detached DOM nodes, event listeners
```

**Common causes:**

1. **Uncleared subscriptions:**
```javascript
// Bad: Memory leak
useEffect(() => {
  const subscription = eventEmitter.subscribe(handler);
  // No cleanup!
}, []);

// Good: Cleanup
useEffect(() => {
  const subscription = eventEmitter.subscribe(handler);
  return () => subscription.unsubscribe();
}, []);
```

2. **Event listeners not removed:**
```javascript
// Bad
useEffect(() => {
  window.addEventListener('resize', handleResize);
}, []);

// Good
useEffect(() => {
  window.addEventListener('resize', handleResize);
  return () => window.removeEventListener('resize', handleResize);
}, []);
```

3. **Timers not cleared:**
```javascript
useEffect(() => {
  const intervalId = setInterval(poll, 5000);
  return () => clearInterval(intervalId);
}, []);
```

4. **Closures holding references:**
```javascript
// Bad: closure holds large data
function setup() {
  const largeData = fetchLargeData();
  element.onclick = () => process(largeData);
}

// Good: Use WeakRef or cleanup
function setup() {
  const largeData = fetchLargeData();
  element.onclick = () => process(largeData);

  return () => {
    element.onclick = null;
  };
}
```

**Prevention patterns:**

```typescript
// AbortController for fetch
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

// Custom hook for safe subscriptions
function useSubscription(subscribe, deps) {
  useEffect(() => {
    const unsubscribe = subscribe();
    return unsubscribe;
  }, deps);
}
```
</details>

<details>
<summary><b>Intermittent API failures only in production — debugging strategy</b></summary>

**Systematic approach:**

1. **Add observability:**
```typescript
// Structured logging
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
      headers: Object.fromEntries(response.headers),
    });

    return response;
  } catch (error) {
    logger.error('api_error', {
      requestId,
      error: error.message,
      stack: error.stack,
      duration: Date.now() - startTime,
    });
    throw error;
  }
}
```

2. **Check for environment differences:**
- CORS configuration (different domains)
- SSL/TLS certificate issues
- CDN caching behavior
- Load balancer timeout settings
- Rate limiting / throttling

3. **Network issues:**
```typescript
// Detect network conditions
navigator.connection?.addEventListener('change', () => {
  logger.info('network_change', {
    effectiveType: navigator.connection.effectiveType,
    downlink: navigator.connection.downlink,
  });
});

// Retry with jitter
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

4. **Server-side correlation:**
```typescript
// Add correlation ID to track requests end-to-end
const correlationId = crypto.randomUUID();

fetch('/api/data', {
  headers: {
    'X-Correlation-ID': correlationId,
    'X-Client-Version': APP_VERSION,
  }
});
```

5. **Use error tracking service:**
- Sentry, Bugsnag, or Datadog
- Track error frequency, user impact, stack traces
- Set up alerts for error rate spikes

**Common production-only issues:**
- DNS resolution failures
- Certificate pinning issues
- Geographic-specific routing problems
- Peak traffic timing issues
- Third-party service degradation
</details>
