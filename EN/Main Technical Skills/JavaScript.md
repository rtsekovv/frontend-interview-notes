# JavaScript Interview Questions

## Scope & Closures

<details>
<summary><b>What is the temporal dead zone and why does it exist?</b></summary>

TDZ is the period between entering scope and variable declaration. Variables declared with `let`/`const` exist in TDZ and cannot be accessed. Purpose: catch errors early, prevent confusing behavior where variable exists but is undefined. Forces cleaner code by requiring declaration before use.
</details>

<details>
<summary><b>What happens with const in a for...of loop?</b></summary>

Works fine because each iteration creates a new binding. The variable is re-declared fresh each iteration, not reassigned:
```javascript
for (const item of [1, 2, 3]) {
  console.log(item); // Works: 1, 2, 3
}
// But this fails:
for (const i = 0; i < 3; i++) { } // Error: Assignment to constant
```
</details>

<details>
<summary><b>What are closures and how do they work?</b></summary>

Closure is a function that remembers variables from its outer scope even after outer function has finished. Inner function "closes over" outer variables. Example:
```javascript
function outer() {
  let count = 0;
  return function inner() { return ++count; };
}
const counter = outer();
counter(); // 1
counter(); // 2 - remembers count
```
</details>

<details>
<summary><b>Explain the different types of scope in JavaScript</b></summary>

- **Global scope**: Variables accessible everywhere
- **Function scope**: Variables inside function, not accessible outside
- **Block scope**: Variables inside `{}` (let, const only)
- **Lexical scope**: Inner functions access outer function variables
</details>

## Hoisting

<details>
<summary><b>What is hoisting in JavaScript?</b></summary>

JavaScript moves declarations to top of their scope before execution. Functions are fully hoisted. `var` declarations hoisted (initialized as undefined). `let`/`const` hoisted but not initialized (temporal dead zone).
</details>

<details>
<summary><b>How does hoisting differ for var, let, and const?</b></summary>

- `var`: Hoisted and initialized as `undefined`. Can access before declaration (get undefined)
- `let`/`const`: Hoisted but NOT initialized. Accessing before declaration throws ReferenceError (temporal dead zone)
</details>

## Strict Mode

<details>
<summary><b>What is strict mode and why should you use it?</b></summary>

`'use strict'` enables stricter parsing. Benefits: prevents accidental globals, throws errors for unsafe actions, disables confusing features. Example: can't use undeclared variables, can't delete variables, no duplicate parameters.
</details>

## Reference vs Value

<details>
<summary><b>What is the difference between passing by reference and by value?</b></summary>

- **By value**: Primitives (string, number, boolean). Copy of value passed. Changes don't affect original
- **By reference**: Objects, arrays. Reference (memory address) passed. Changes affect original object
</details>

## JavaScript Types

<details>
<summary><b>What are the primitive types in JavaScript?</b></summary>

7 primitives: `string`, `number`, `boolean`, `null`, `undefined`, `symbol`, `bigint`. Primitives are immutable and compared by value.
</details>

<details>
<summary><b>What is the difference between null and undefined?</b></summary>

- `undefined`: Variable declared but not assigned. Default return value. Parameter not passed
- `null`: Intentional absence of value. Explicitly assigned by developer
- `typeof null === 'object'` (historical bug)
</details>

<details>
<summary><b>How does equality work in JS? What is the difference between === and Object.is()?</b></summary>

Both `===` and `Object.is()` check strict equality, but they differ in edge cases:

| Comparison | `===` | `Object.is()` |
|------------|-------|---------------|
| `NaN === NaN` | `false` | `true` |
| `+0 === -0` | `true` | `false` |
| Everything else | Same | Same |

```javascript
NaN === NaN          // false
Object.is(NaN, NaN)  // true

+0 === -0            // true
Object.is(+0, -0)    // false
```

`Object.is()` is the "same value" algorithm - useful when you need mathematically correct comparison. Used internally by React for state comparison.
</details>

## let, const, and var

<details>
<summary><b>What are the differences between let, const, and var?</b></summary>

- `var`: Function scoped, hoisted, can redeclare, can reassign
- `let`: Block scoped, temporal dead zone, can't redeclare, can reassign
- `const`: Block scoped, temporal dead zone, can't redeclare, can't reassign (but object properties can change)
</details>

## Functions

<details>
<summary><b>What is function currying?</b></summary>

Currying transforms function with multiple arguments into sequence of functions each taking one argument. `f(a, b, c)` becomes `f(a)(b)(c)`. Useful for: partial application, creating specialized functions, functional composition.
```javascript
const add = a => b => a + b;
const add5 = add(5);
add5(3); // 8
```
</details>

<details>
<summary><b>What is partial application?</b></summary>

Creating new function by pre-filling some arguments of existing function. Similar to currying but fixes specific arguments:
```javascript
const multiply = (a, b, c) => a * b * c;
const double = multiply.bind(null, 2, 1); // a=2, b=1 fixed
double(5); // 10
```
</details>

<details>
<summary><b>What are higher-order functions?</b></summary>

Functions that take functions as arguments or return functions. Examples: `map`, `filter`, `reduce`, `forEach`. Enable functional programming patterns, code reuse, and abstraction.
```javascript
const withLogging = fn => (...args) => {
  console.log('Calling with', args);
  return fn(...args);
};
```
</details>

<details>
<summary><b>What is function composition?</b></summary>

Combining simple functions to build complex ones. Output of one function becomes input of next:
```javascript
const compose = (f, g) => x => f(g(x));
const addOne = x => x + 1;
const double = x => x * 2;
const addOneThenDouble = compose(double, addOne);
addOneThenDouble(3); // 8
```
</details>

<details>
<summary><b>How do default parameters work?</b></summary>

Set fallback values when argument is undefined:
```javascript
function greet(name = 'Guest', greeting = 'Hello') {
  return `${greeting}, ${name}`;
}
greet(); // "Hello, Guest"
greet('John'); // "Hello, John"
```
Default params are evaluated at call time, left-to-right. Can reference previous params.
</details>

<details>
<summary><b>What is the difference between anonymous and declarative functions?</b></summary>

- **Declarative** (function declaration): Has name, hoisted. `function foo() {}`
- **Anonymous**: No name, assigned to variable or passed as callback. `const foo = function() {}`
</details>

<details>
<summary><b>What are arrow functions and how do they differ from regular functions?</b></summary>

Arrow functions: shorter syntax `() => {}`. Differences:
- No own `this` - inherits from parent scope
- No `arguments` object
- Can't be used as constructors (no `new`)
- No `prototype` property
- Can't be generators
</details>

## Exception Handling

<details>
<summary><b>How do you handle exceptions in JavaScript?</b></summary>

Use `try...catch...finally`. `try` contains risky code, `catch` handles errors, `finally` always runs. Throw custom errors with `throw new Error('message')`. For async: `.catch()` for promises, try/catch with async/await.
</details>

## Loops

<details>
<summary><b>What loop types are available in JavaScript?</b></summary>

`for`, `while`, `do...while`, `for...in` (object keys), `for...of` (iterable values), `forEach` (arrays). Use `break` to exit, `continue` to skip iteration.
</details>

<details>
<summary><b>What is the difference between for...in and for...of?</b></summary>

- `for...in`: Iterates over object keys/indices. Works on objects. Can iterate inherited properties
- `for...of`: Iterates over values. Works on iterables (arrays, strings, Maps, Sets). Cleaner for arrays
</details>

## Context (call, apply, bind)

<details>
<summary><b>Explain call, apply, and bind methods</b></summary>

- `call(thisArg, arg1, arg2)`: Invoke function with specific `this`, args passed individually
- `apply(thisArg, [args])`: Same as call, but args as array
- `bind(thisArg, arg1)`: Returns new function with `this` bound permanently. Doesn't invoke immediately
</details>

<details>
<summary><b>How does 'this' work in JavaScript?</b></summary>

`this` depends on how function is called:
- Method call: `this` = object before dot
- Regular function: `this` = global (or undefined in strict mode)
- Arrow function: `this` = inherited from parent scope
- Constructor: `this` = new object
- Event handler: `this` = element that received event
</details>

## Map and Set

<details>
<summary><b>What is the difference between Map and Object?</b></summary>

- **Map**: Any type as key, maintains insertion order, has `size` property, iterable, better for frequent add/remove
- **Object**: Only string/symbol keys, no guaranteed order, need `Object.keys().length` for size
</details>

<details>
<summary><b>When would you use Set over an Array?</b></summary>

Use Set when you need: unique values only, fast `has()` checks, remove duplicates from array (`[...new Set(arr)]`). Sets are faster for lookup operations.
</details>

## Rest & Spread Operators

<details>
<summary><b>Explain rest and spread operators</b></summary>

Both use `...` but different purposes:
- **Spread**: Expand array/object. `[...arr1, ...arr2]`, `{...obj1, ...obj2}`
- **Rest**: Collect remaining items. `function(a, ...rest)`, `const [first, ...rest] = arr`
</details>

## Promises

<details>
<summary><b>What is callback hell and how do you avoid it?</b></summary>

Deeply nested callbacks creating pyramid-shaped code. Hard to read, debug, handle errors. Solutions: Promises with `.then()` chains, async/await syntax, breaking into named functions, using Promise.all for parallel operations.
</details>

<details>
<summary><b>What is Promise.all vs Promise.allSettled?</b></summary>

- `Promise.all()`: Resolves when ALL promises resolve. Rejects immediately if ANY promise rejects
- `Promise.allSettled()`: Waits for ALL promises to complete (resolve or reject). Returns array with status and value/reason for each

Use `allSettled` when you need results regardless of individual failures.
</details>

<details>
<summary><b>When would you use Promise.race?</b></summary>

Returns result of first promise to settle (resolve or reject). Use cases: timeout patterns, fastest response wins, racing multiple data sources:
```javascript
const timeout = new Promise((_, reject) =>
  setTimeout(() => reject('Timeout'), 5000)
);
Promise.race([fetchData(), timeout]);
```
</details>

<details>
<summary><b>How does Promise.any differ from Promise.race?</b></summary>

- `Promise.race()`: Settles with first promise to settle (resolve OR reject)
- `Promise.any()`: Resolves with first promise to FULFILL. Only rejects if ALL promises reject (AggregateError)

Use `any` when you want first successful result, ignoring failures.
</details>

<details>
<summary><b>Can you use await outside of async functions?</b></summary>

Yes, in ES modules (top-level await). Works in `.mjs` files or with `"type": "module"` in package.json:
```javascript
// module.mjs
const data = await fetch('/api').then(r => r.json());
export { data };
```
Not available in CommonJS or regular scripts.
</details>

<details>
<summary><b>What happens if you don't await an async function?</b></summary>

Returns Promise immediately. Function runs in background. Errors may go unhandled (unhandled rejection). Use when you don't need the result, but always handle errors:
```javascript
asyncFunction().catch(console.error); // Fire and forget safely
```
</details>

<details>
<summary><b>How do you cancel a Promise?</b></summary>

Promises themselves can't be cancelled. Use AbortController for fetch:
```javascript
const controller = new AbortController();
fetch(url, { signal: controller.signal });
controller.abort(); // Cancels the fetch
```
For custom promises, use cancellation tokens or check flag before resolving.
</details>

<details>
<summary><b>What are async iterators?</b></summary>

Allow iterating over async data sources with `for await...of`:
```javascript
async function* asyncGenerator() {
  yield await fetch('/api/1').then(r => r.json());
  yield await fetch('/api/2').then(r => r.json());
}
for await (const data of asyncGenerator()) {
  console.log(data);
}
```
Useful for streaming data, paginated APIs, WebSocket messages.
</details>

<details>
<summary><b>What are Promises and how do they work?</b></summary>

Promise represents eventual completion/failure of async operation. States: pending → fulfilled/rejected. Use `.then()` for success, `.catch()` for error, `.finally()` for cleanup. Create with `new Promise((resolve, reject) => {})`.
</details>

<details>
<summary><b>What is Promise chaining?</b></summary>

Connect multiple `.then()` calls. Each `.then()` returns new Promise. Value returned from one becomes input to next. Errors propagate down to nearest `.catch()`. Cleaner than callback nesting.
</details>

## Date & Math

<details>
<summary><b>How do you work with dates in JavaScript?</b></summary>

`new Date()` creates date object. Methods: `getFullYear()`, `getMonth()` (0-11), `getDate()`, `getTime()` (timestamp). For complex operations use libraries like date-fns or dayjs.
</details>

<details>
<summary><b>What are common Math methods you use?</b></summary>

`Math.round()`, `Math.floor()`, `Math.ceil()`, `Math.random()` (0-1), `Math.max()`, `Math.min()`, `Math.abs()`, `Math.pow()`, `Math.sqrt()`.
</details>

## Object

<details>
<summary><b>How do you iterate over object properties?</b></summary>

- `Object.keys(obj)` - array of keys
- `Object.values(obj)` - array of values
- `Object.entries(obj)` - array of [key, value] pairs
- `for...in` loop (includes inherited)
</details>

<details>
<summary><b>What is Object.freeze vs Object.seal?</b></summary>

- `Object.freeze()`: Can't add, remove, or modify properties. Shallow freeze
- `Object.seal()`: Can't add or remove properties, but CAN modify existing ones
</details>

## HTTP / HTTPS

<details>
<summary><b>What is the difference between HTTP and HTTPS?</b></summary>

HTTP is a basic web communication protocol. HTTPS adds encryption (TLS/SSL) and security. Modern websites require HTTPS for: security, SEO ranking, browser features (geolocation, service workers), user trust.
</details>

## Web Sockets

<details>
<summary><b>What are WebSockets and when would you use them?</b></summary>

WebSocket provides full-duplex communication channel over single TCP connection. Server can push data to client without request. Use for: real-time apps, chat, live feeds, gaming, collaborative editing. More efficient than polling.
</details>

<details>
<summary><b>What are Server-Sent Events (SSE) and how do they differ from WebSockets?</b></summary>

SSE is a server push technology for one-way communication from server to client over HTTP.

**SSE characteristics:**
- One-directional (server → client only)
- Built on HTTP, simpler than WebSockets
- Automatic reconnection
- Text-based (UTF-8)
- Built-in browser support via `EventSource` API

**Usage:**
```javascript
const eventSource = new EventSource('/events');
eventSource.onmessage = (event) => console.log(event.data);
eventSource.onerror = () => console.log('Connection error');
```

**SSE vs WebSockets:**
| Feature | SSE | WebSocket |
|---------|-----|-----------|
| Direction | Server → Client | Bidirectional |
| Protocol | HTTP | WS/WSS |
| Complexity | Simple | More complex |
| Reconnection | Automatic | Manual |
| Data format | Text only | Text + Binary |

Use SSE for: live feeds, notifications, stock tickers. Use WebSockets for: chat, gaming, collaborative editing.
</details>

## Functional Programming

<details>
<summary><b>What are the principles of functional programming?</b></summary>

- Pure functions (no side effects)
- Immutability (don't mutate data)
- First-class functions (functions as values)
- Higher-order functions (map, filter, reduce)
- Avoid shared state
- Declarative over imperative
</details>

<details>
<summary><b>What are pure functions?</b></summary>

Pure function: same input always gives same output, no side effects (doesn't modify external state). Easy to test, predictable, cacheable. Example: `const add = (a, b) => a + b`.
</details>

## OOP & Prototypes

<details>
<summary><b>Explain prototype inheritance in JavaScript</b></summary>

Every object has hidden `[[Prototype]]` linking to another object. When property not found, JS looks up prototype chain. `Object.create(proto)` creates object with specific prototype. Classes are syntactic sugar over prototypes.
</details>

<details>
<summary><b>What is the difference between __proto__ and prototype?</b></summary>

**`__proto__`** - exists on every object:
- Reference to the object's prototype
- Used at runtime for property lookup
- `obj.__proto__ === Constructor.prototype`

**`prototype`** - exists only on functions (constructors):
- Object that becomes `__proto__` of instances created with `new`
- Used to add methods shared by all instances

```javascript
function Player(name) {
  this.name = name;
}
Player.prototype.play = function() { console.log('play'); };

const p1 = new Player('Alex');
p1.__proto__ === Player.prototype; // true
```

**Prototype chain lookup:**
1. Check the object itself
2. Check `__proto__`
3. Check `__proto__.__proto__`
4. Continue until `null`

**Important notes:**
- Don't use `__proto__` directly - use `Object.getPrototypeOf()` / `Object.setPrototypeOf()`
- Changing prototype after object creation is slow
- Classes are syntactic sugar - `class` methods go to `Constructor.prototype`

**Interview one-liner:** `prototype` is a property of constructor functions that defines shared methods, while `__proto__` is every object's reference to its prototype used for inheritance lookup.
</details>

<details>
<summary><b>How do classes and super work?</b></summary>

`class` syntax for creating objects. `constructor()` initializes instance. `extends` for inheritance. `super()` calls parent constructor (required in child constructor before using `this`). `super.method()` calls parent method.
</details>

<details>
<summary><b>How do ES6 classes relate to prototypes?</b></summary>

Classes are syntactic sugar over prototypes. Under the hood:
- Class methods go to `Constructor.prototype`
- `extends` sets up prototype chain
- `super()` calls parent constructor with correct `this`

Same behavior as prototype-based inheritance, cleaner syntax.
</details>

<details>
<summary><b>What are static methods in classes?</b></summary>

Methods on the class itself, not instances. Called on class name, not `this`. Use for utility functions, factory methods:
```javascript
class MathUtils {
  static square(x) { return x * x; }
}
MathUtils.square(5); // 25
// Not: new MathUtils().square(5)
```
</details>

<details>
<summary><b>Can you extend built-in objects? Should you?</b></summary>

Technically possible: `class MyArray extends Array {}`. Generally avoid: can break future JS features, causes confusion, harder to debug. Better approach: composition (wrap built-ins) or utility functions.
</details>

## Async & Performance

<details>
<summary><b>Explain the concurrency model and event loop</b></summary>

JS is single-threaded. Event loop handles async operations. Call stack executes code. Web APIs handle async tasks. Task queue (macrotasks) and microtask queue. Microtasks (promises) run before macrotasks (setTimeout). Event loop moves tasks to stack when empty.
</details>

<details>
<summary><b>What are async and await?</b></summary>

Syntactic sugar over Promises. `async` function always returns Promise. `await` pauses execution until Promise resolves. Cleaner than `.then()` chains. Use `try/catch` for error handling. Can only use `await` inside `async` function.
</details>

<details>
<summary><b>What is Promise optimization and promisification?</b></summary>

- **Promise.all()**: Run promises in parallel, fail if any fails
- **Promise.allSettled()**: Wait for all, get all results
- **Promise.race()**: First to complete wins
- **Promisification**: Convert callback-based function to return Promise
</details>

## Destructuring & Template Strings

<details>
<summary><b>Explain destructuring assignment</b></summary>

Extract values from arrays/objects into variables. Arrays: `const [a, b] = [1, 2]`. Objects: `const {name, age} = user`. Can set defaults: `const {name = 'unknown'} = obj`. Nested destructuring possible.
</details>

<details>
<summary><b>What are template strings/literals?</b></summary>

Strings with backticks. Features: embed expressions `${variable}`, multi-line strings, tagged templates. Example: `` `Hello ${name}, you are ${age} years old` ``.
</details>

## Modules

<details>
<summary><b>How do import and export work in JavaScript?</b></summary>

- Named export: `export const foo = 1;` → `import { foo } from './file'`
- Default export: `export default function() {}` → `import myFunc from './file'`
- Can rename: `import { foo as bar } from './file'`
- Import all: `import * as utils from './file'`
</details>

<details>
<summary><b>What is the difference between CommonJS and ES modules?</b></summary>

- **CommonJS**: `require()`/`module.exports`, synchronous, Node.js, dynamic
- **ES modules**: `import`/`export`, async, static (allows tree shaking), modern standard
</details>

## Proxy & Reflect

<details>
<summary><b>What is a Proxy in JavaScript?</b></summary>

Proxy wraps object and intercepts operations. Define custom behavior for: get, set, delete, function calls, etc. Use for: validation, logging, data binding, negative array indices.
</details>

<details>
<summary><b>What is Reflect and how is it used?</b></summary>

Reflect provides methods for interceptable operations. Same methods as Proxy handlers. Cleaner than Object methods. Example: `Reflect.get(obj, 'prop')`, `Reflect.set(obj, 'prop', value)`.
</details>

## WeakMap & WeakSet

<details>
<summary><b>What is the difference between WeakMap and Map?</b></summary>

- **WeakMap**: Only objects as keys, keys are weakly held (garbage collected if no other references), not iterable, no `size`
- Use for: private data, caching without memory leaks
</details>

<details>
<summary><b>When would you use WeakSet?</b></summary>

Store objects without preventing garbage collection. Use for: tracking visited objects, marking objects as processed. Items automatically removed when object has no other references.
</details>

## Regular Expressions

<details>
<summary><b>How do you use regular expressions in JavaScript?</b></summary>

Create: `/pattern/flags` or `new RegExp()`. Methods: `test()` returns boolean, `match()` returns matches, `replace()` replaces. Flags: `g` (global), `i` (case-insensitive), `m` (multiline).
</details>

## Web Workers & Service Workers

<details>
<summary><b>What are Web Workers?</b></summary>

Run scripts in background thread. Don't block UI. Can't access DOM. Communicate via `postMessage()`. Use for: heavy calculations, data processing.
</details>

<details>
<summary><b>What are Service Workers and how are they different?</b></summary>

Special workers that act as proxy between app and network. Enable: offline support, caching, push notifications, background sync. Lifecycle: install → activate → fetch. **Require HTTPS** (except localhost). Required for PWAs.
</details>

## Dependency Injection

<details>
<summary><b>Explain different module systems (CommonJS, AMD, namespace)</b></summary>

- **CommonJS**: `require/exports`, synchronous, Node.js
- **AMD**: `define/require`, asynchronous, browser (RequireJS)
- **Namespace**: Global object pattern, old approach. `MyApp.utils.foo()`
</details>

## Storage

<details>
<summary><b>What is the difference between LocalStorage and SessionStorage?</b></summary>

- **LocalStorage**: Persists until manually cleared, ~5MB, same-origin
- **SessionStorage**: Cleared when tab closes, per-tab isolation
- Both: synchronous, strings only (use JSON.stringify)
</details>

<details>
<summary><b>What is the difference between Cookies, sessionStorage, and localStorage?</b></summary>

- **Cookies**: Sent with every HTTP request, support security options (HttpOnly, Secure, SameSite), max ~4KB, can set expiry
- **sessionStorage**: Lasts until the tab is closed, ~5MB, not sent to server
- **localStorage**: Saves data permanently in the browser, ~5MB, not sent to server

Use cookies for auth tokens (with HttpOnly), storage APIs for client-side data.
</details>

## Memory Management

<details>
<summary><b>How does garbage collection work in JavaScript?</b></summary>

Automatic memory management. Mark-and-sweep algorithm: marks reachable objects, sweeps unmarked. Runs periodically. Objects with no references are collected.
</details>

<details>
<summary><b>How do you prevent memory leaks?</b></summary>

Common causes and fixes:
- Remove event listeners when done
- Clear intervals/timeouts
- Avoid global variables
- Clean up closures
- Null out references to large objects
- Use WeakMap/WeakSet for caches
</details>

## Generators & Iterators

<details>
<summary><b>What are generators and how do you use them?</b></summary>

Functions that can pause and resume. Use `function*` and `yield`. Returns iterator. `next()` continues execution. Use for: lazy evaluation, infinite sequences, async flows.
</details>

<details>
<summary><b>What are iterators?</b></summary>

Object with `next()` method returning `{value, done}`. Makes object iterable with `for...of`. Implement `[Symbol.iterator]` to make custom iterables.
</details>

## Type Coercion

<details>
<summary><b>What does !!variable do?</b></summary>

Double negation converts value to boolean. First `!` converts to boolean and negates, second `!` negates back. Same as `Boolean(value)`:
```javascript
!!0        // false
!!"hello"  // true
!!null     // false
!!{}       // true
```
</details>

<details>
<summary><b>What is the result of [] + {} vs {} + []?</b></summary>

```javascript
[] + {}  // "[object Object]" - array to "", object to string
{} + []  // 0 - {} is empty block, +[] is 0
```
Tricky because `{}` at start is parsed as code block, not object. Wrap in parens: `({}) + []` gives "[object Object]".
</details>

<details>
<summary><b>How do you safely check for null and undefined?</b></summary>

```javascript
// Check both (loose equality)
if (value == null) { } // catches null and undefined

// Nullish coalescing (ES2020)
const result = value ?? 'default'; // only null/undefined

// Optional chaining
const name = user?.profile?.name;
```
</details>

<details>
<summary><b>How does Number() differ from parseInt()?</b></summary>

- `Number()`: Converts entire string, returns NaN if any non-numeric char
- `parseInt()`: Parses from start, stops at non-numeric, ignores leading whitespace

```javascript
Number("42px")   // NaN
parseInt("42px") // 42
Number("")       // 0
parseInt("")     // NaN
```
</details>

## Array Methods Advanced

<details>
<summary><b>What's the Big O complexity of chaining array methods?</b></summary>

Each method iterates entire array: O(n) per method. Chaining `map().filter().reduce()` = O(3n) = O(n), but with 3x iterations. For large arrays, consider single `reduce()` or for-loop to process in one pass.
</details>

<details>
<summary><b>What happens if you don't return anything from a map callback?</b></summary>

Returns `undefined` for that element. Array length stays same, but values are undefined:
```javascript
[1, 2, 3].map(x => { x * 2 }); // [undefined, undefined, undefined]
[1, 2, 3].map(x => x * 2);      // [2, 4, 6]
```
Common mistake: forgetting return in multi-line arrow functions.
</details>

<details>
<summary><b>What are flatMap and flat methods?</b></summary>

- `flat(depth)`: Flattens nested arrays by depth (default 1)
- `flatMap(fn)`: Maps then flattens one level. More efficient than `.map().flat()`

```javascript
[[1], [2, 3]].flat();           // [1, 2, 3]
[1, 2].flatMap(x => [x, x*2]);  // [1, 2, 2, 4]
```
</details>

<details>
<summary><b>How do you sort objects by a property?</b></summary>

Pass compare function to sort:
```javascript
const users = [{name: 'Bob', age: 30}, {name: 'Alice', age: 25}];
users.sort((a, b) => a.age - b.age); // By age ascending
users.sort((a, b) => a.name.localeCompare(b.name)); // By name
```
Note: `sort()` mutates original array.
</details>

## Symbols

<details>
<summary><b>What are Symbols and when would you use them?</b></summary>

Unique, immutable primitive. `Symbol('description')`. Use for: private-ish properties, avoid name collisions, well-known symbols (`Symbol.iterator`, `Symbol.toStringTag`).
</details>

<details>
<summary><b>What is a Symbol?</b></summary>

A Symbol is a unique value used as a property key in objects. It helps prevent name conflicts, especially in shared code like libraries. Each Symbol is always different, even if it has the same name. `Symbol('a') !== Symbol('a')`.
</details>

## Iterators

<details>
<summary><b>What are Iterators?</b></summary>

An iterator is an object that lets you read values one by one. It follows a simple rule using a `next()` method that returns `{value, done}`. Iterators are used in `for...of` loops and other built-in features like spread operator.
</details>

## NaN

<details>
<summary><b>What is NaN?</b></summary>

NaN means "Not a Number." It appears when a calculation fails (e.g., `0/0`, `parseInt('abc')`). NaN is special because it is not equal to itself (`NaN !== NaN`). Use `Number.isNaN()` to check for NaN.
</details>

## IIFE

<details>
<summary><b>What is an IIFE?</b></summary>

An IIFE (Immediately Invoked Function Expression) is a function that runs immediately after it is defined. It was used to create private variables before modern syntax existed. Example: `(function() { var private = 1; })()`. It is mostly seen in older code now.
</details>

## Event Loop

<details>
<summary><b>What is the Event Loop?</b></summary>

The event loop controls the order in which JavaScript code runs. It handles synchronous code first, then microtasks (promises), then macrotasks (setTimeout, setInterval). This allows JavaScript to be non-blocking despite being single-threaded.
</details>

## DOM

<details>
<summary><b>What is the DOM?</b></summary>

The DOM (Document Object Model) represents a web page as a tree structure. JavaScript uses it to read and update the UI. DOM operations can be slow if overused - that's why frameworks like React use Virtual DOM.
</details>

## Event Bubbling

<details>
<summary><b>What is Event Bubbling?</b></summary>

Events move from the target element up to parent elements. This allows event delegation - attach one listener to parent instead of many to children. Bubbling can be stopped with `event.stopPropagation()` when needed.
</details>

## JSONP

<details>
<summary><b>What is JSONP?</b></summary>

JSONP is an old technique to load data across domains before CORS existed. It uses script tags and callbacks. It is insecure (executes arbitrary code) and rarely used today. CORS is the modern solution.
</details>

## Immutability

<details>
<summary><b>What is Immutability?</b></summary>

Immutability means not changing existing data. Instead, new data is created. This makes state changes easier to track and debug. Example: instead of `arr.push(item)`, use `[...arr, item]`. Important for React state management.
</details>

## File APIs

<details>
<summary><b>What is the FileSystem API?</b></summary>

Browser API to read/write files to sandboxed file system. Limited browser support. Modern File System Access API allows accessing user's files with permission.
</details>

<details>
<summary><b>What is the FileReader API?</b></summary>

Read file contents asynchronously. Methods: `readAsText()`, `readAsDataURL()`, `readAsArrayBuffer()`. Events: `onload`, `onerror`. Use with file input or drag-drop.
</details>

## GraphQL

<details>
<summary><b>What is GraphQL?</b></summary>

GraphQL lets clients request exactly the data they need. It uses a single endpoint instead of multiple REST endpoints. Benefits: no over-fetching/under-fetching, strongly typed schema, introspection. Trade-off: adds server complexity, caching is harder than REST.
</details>

## Design Patterns

<details>
<summary><b>What design patterns do you use in JavaScript?</b></summary>

Common patterns:
- **Module**: Encapsulate code, private/public
- **Singleton**: Single instance
- **Observer**: Publish/subscribe events
- **Factory**: Create objects without specifying class
- **Decorator**: Add behavior to objects
</details>

## Advanced Event Loop

<details>
<summary><b>Explain event loop behavior with nested promises + setTimeout + async/await</b></summary>

```javascript
console.log('1');
setTimeout(() => console.log('2'), 0);
Promise.resolve().then(() => {
  console.log('3');
  Promise.resolve().then(() => console.log('4'));
});
async function foo() {
  console.log('5');
  await Promise.resolve();
  console.log('6');
}
foo();
console.log('7');
// Output: 1, 5, 7, 3, 6, 4, 2
```

**Order of execution:**
1. Synchronous code runs first (1, 5, 7)
2. `await` pauses `foo()`, schedules continuation as microtask
3. Microtasks run before macrotasks: promise callbacks (3), then `foo` continuation (6), then nested promise (4)
4. Macrotasks (setTimeout) run last (2)

**Key rule:** Microtask queue (promises) is fully drained before each macrotask (setTimeout, setInterval).
</details>

## Utility Function Implementations

<details>
<summary><b>Implement debounce, throttle, and memoize functions</b></summary>

**Debounce** - delays execution until pause in calls:
```javascript
function debounce(fn, delay) {
  let timeoutId;
  return function(...args) {
    clearTimeout(timeoutId);
    timeoutId = setTimeout(() => fn.apply(this, args), delay);
  };
}
```

**Throttle** - limits execution to once per time period:
```javascript
function throttle(fn, limit) {
  let inThrottle;
  return function(...args) {
    if (!inThrottle) {
      fn.apply(this, args);
      inThrottle = true;
      setTimeout(() => inThrottle = false, limit);
    }
  };
}
```

**Memoize** - caches function results:
```javascript
function memoize(fn) {
  const cache = new Map();
  return function(...args) {
    const key = JSON.stringify(args);
    if (cache.has(key)) return cache.get(key);
    const result = fn.apply(this, args);
    cache.set(key, result);
    return result;
  };
}
```
</details>

<details>
<summary><b>Implement a custom curry function</b></summary>

Currying transforms `f(a, b, c)` into `f(a)(b)(c)`:

```javascript
function curry(fn) {
  return function curried(...args) {
    if (args.length >= fn.length) {
      return fn.apply(this, args);
    }
    return function(...nextArgs) {
      return curried.apply(this, args.concat(nextArgs));
    };
  };
}

// Usage
const sum = (a, b, c) => a + b + c;
const curriedSum = curry(sum);
curriedSum(1)(2)(3); // 6
curriedSum(1, 2)(3); // 6
curriedSum(1)(2, 3); // 6
```
</details>

<details>
<summary><b>Write a deep clone function without using lodash</b></summary>

```javascript
function deepClone(obj, seen = new WeakMap()) {
  // Handle primitives and null
  if (obj === null || typeof obj !== 'object') return obj;

  // Handle circular references
  if (seen.has(obj)) return seen.get(obj);

  // Handle Date
  if (obj instanceof Date) return new Date(obj);

  // Handle RegExp
  if (obj instanceof RegExp) return new RegExp(obj);

  // Handle Array and Object
  const clone = Array.isArray(obj) ? [] : {};
  seen.set(obj, clone);

  for (const key in obj) {
    if (obj.hasOwnProperty(key)) {
      clone[key] = deepClone(obj[key], seen);
    }
  }

  return clone;
}
```

**Edge cases handled:** circular references, Date, RegExp, nested objects/arrays. Note: doesn't handle Map, Set, functions, or prototype chain.
</details>

<details>
<summary><b>What happens internally when you call `new`?</b></summary>

When `new Constructor()` is called:

1. **Create empty object**: `const obj = {}`
2. **Link prototype**: `obj.__proto__ = Constructor.prototype`
3. **Bind `this`**: Execute constructor with `this` bound to `obj`
4. **Return object**: Return `obj` (unless constructor returns different object)

```javascript
function myNew(Constructor, ...args) {
  // 1. Create new object
  const obj = {};
  // 2. Link prototype
  Object.setPrototypeOf(obj, Constructor.prototype);
  // 3. Execute constructor with this = obj
  const result = Constructor.apply(obj, args);
  // 4. Return object (or constructor's return if it's an object)
  return result instanceof Object ? result : obj;
}
```
</details>

<details>
<summary><b>Implement your own Promise.all, Promise.race, Promise.any</b></summary>

```javascript
// Promise.all - resolves when all resolve, rejects on first rejection
Promise.myAll = function(promises) {
  return new Promise((resolve, reject) => {
    const results = [];
    let completed = 0;
    promises.forEach((promise, index) => {
      Promise.resolve(promise).then(value => {
        results[index] = value;
        if (++completed === promises.length) resolve(results);
      }).catch(reject);
    });
    if (promises.length === 0) resolve([]);
  });
};

// Promise.race - resolves/rejects with first settled
Promise.myRace = function(promises) {
  return new Promise((resolve, reject) => {
    promises.forEach(promise => {
      Promise.resolve(promise).then(resolve).catch(reject);
    });
  });
};

// Promise.any - resolves with first fulfilled, rejects if all reject
Promise.myAny = function(promises) {
  return new Promise((resolve, reject) => {
    const errors = [];
    let rejected = 0;
    promises.forEach((promise, index) => {
      Promise.resolve(promise)
        .then(resolve)
        .catch(error => {
          errors[index] = error;
          if (++rejected === promises.length) {
            reject(new AggregateError(errors, 'All promises rejected'));
          }
        });
    });
    if (promises.length === 0) reject(new AggregateError([], 'Empty'));
  });
};
```
</details>

<details>
<summary><b>How would you design a plugin system using closures?</b></summary>

```javascript
function createPluginSystem() {
  const plugins = new Map();
  const hooks = {};

  return {
    register(name, plugin) {
      plugins.set(name, plugin);
      if (plugin.init) plugin.init(this);
    },

    unregister(name) {
      const plugin = plugins.get(name);
      if (plugin?.destroy) plugin.destroy();
      plugins.delete(name);
    },

    addHook(event, callback) {
      hooks[event] = hooks[event] || [];
      hooks[event].push(callback);
    },

    async executeHook(event, data) {
      const callbacks = hooks[event] || [];
      let result = data;
      for (const cb of callbacks) {
        result = await cb(result);
      }
      return result;
    },

    getPlugin(name) {
      return plugins.get(name);
    }
  };
}

// Usage
const app = createPluginSystem();
app.register('logger', {
  init(system) {
    system.addHook('beforeRequest', (data) => {
      console.log('Request:', data);
      return data;
    });
  }
});
```
</details>

## Advanced Async Patterns

<details>
<summary><b>Implement API retry with exponential backoff</b></summary>

```javascript
async function fetchWithRetry(url, options = {}, maxRetries = 3) {
  let lastError;

  for (let attempt = 0; attempt < maxRetries; attempt++) {
    try {
      const response = await fetch(url, options);
      if (!response.ok) throw new Error(`HTTP ${response.status}`);
      return response;
    } catch (error) {
      lastError = error;

      // Don't retry on client errors (4xx)
      if (error.message?.includes('4')) throw error;

      // Exponential backoff: 1s, 2s, 4s...
      const delay = Math.pow(2, attempt) * 1000;
      const jitter = Math.random() * 1000; // Add randomness

      console.log(`Retry ${attempt + 1}/${maxRetries} in ${delay}ms`);
      await new Promise(r => setTimeout(r, delay + jitter));
    }
  }

  throw lastError;
}
```
</details>

<details>
<summary><b>How to cancel ongoing API calls during route change?</b></summary>

Use **AbortController** to cancel fetch requests:

```javascript
// Create controller per route/component
const controller = new AbortController();

// Pass signal to fetch
fetch('/api/data', { signal: controller.signal })
  .then(res => res.json())
  .catch(err => {
    if (err.name === 'AbortError') {
      console.log('Request cancelled');
    }
  });

// Cancel on route change/cleanup
controller.abort();

// React example
useEffect(() => {
  const controller = new AbortController();

  fetch('/api/data', { signal: controller.signal })
    .then(res => res.json())
    .then(setData);

  return () => controller.abort(); // Cleanup
}, []);
```

For multiple requests, create new controller per batch or use a request manager.
</details>

<details>
<summary><b>Design a caching layer for frequently accessed APIs</b></summary>

```javascript
class APICache {
  constructor(ttl = 60000) { // Default 1 minute TTL
    this.cache = new Map();
    this.ttl = ttl;
  }

  async fetch(url, options = {}) {
    const key = this.createKey(url, options);
    const cached = this.cache.get(key);

    // Return cached if valid
    if (cached && Date.now() < cached.expiry) {
      return cached.data;
    }

    // Fetch fresh data
    const response = await fetch(url, options);
    const data = await response.json();

    // Cache result
    this.cache.set(key, {
      data,
      expiry: Date.now() + this.ttl
    });

    return data;
  }

  createKey(url, options) {
    return `${options.method || 'GET'}:${url}:${JSON.stringify(options.body || '')}`;
  }

  invalidate(pattern) {
    for (const key of this.cache.keys()) {
      if (key.includes(pattern)) this.cache.delete(key);
    }
  }

  clear() {
    this.cache.clear();
  }
}
```

Consider: LRU eviction, stale-while-revalidate, cache tags for grouped invalidation.
</details>

<details>
<summary><b>How to batch multiple API calls into one?</b></summary>

```javascript
class RequestBatcher {
  constructor(batchFn, { delay = 50, maxSize = 100 } = {}) {
    this.batchFn = batchFn;
    this.delay = delay;
    this.maxSize = maxSize;
    this.queue = [];
    this.timeout = null;
  }

  add(item) {
    return new Promise((resolve, reject) => {
      this.queue.push({ item, resolve, reject });

      if (this.queue.length >= this.maxSize) {
        this.flush();
      } else if (!this.timeout) {
        this.timeout = setTimeout(() => this.flush(), this.delay);
      }
    });
  }

  async flush() {
    clearTimeout(this.timeout);
    this.timeout = null;

    const batch = this.queue.splice(0, this.maxSize);
    if (batch.length === 0) return;

    try {
      const items = batch.map(b => b.item);
      const results = await this.batchFn(items);
      batch.forEach((b, i) => b.resolve(results[i]));
    } catch (error) {
      batch.forEach(b => b.reject(error));
    }
  }
}

// Usage - batch user fetches
const userBatcher = new RequestBatcher(
  async (ids) => fetch(`/api/users?ids=${ids.join(',')}`).then(r => r.json())
);

// These will be batched into single request
userBatcher.add(1).then(user => console.log(user));
userBatcher.add(2).then(user => console.log(user));
```
</details>

## Coding Challenges

<details>
<summary><b>Create a mini SPA router in JavaScript</b></summary>

```javascript
class Router {
  constructor() {
    this.routes = {};
    this.currentPath = '';

    window.addEventListener('popstate', () => this.navigate(location.pathname, false));
    document.addEventListener('click', e => {
      if (e.target.matches('[data-link]')) {
        e.preventDefault();
        this.navigate(e.target.getAttribute('href'));
      }
    });
  }

  addRoute(path, handler) {
    // Convert /users/:id to regex
    const pattern = path.replace(/:\w+/g, '([^/]+)');
    this.routes[path] = {
      regex: new RegExp(`^${pattern}$`),
      handler,
      paramNames: (path.match(/:\w+/g) || []).map(p => p.slice(1))
    };
  }

  navigate(path, pushState = true) {
    if (pushState) history.pushState(null, '', path);
    this.currentPath = path;

    for (const [routePath, route] of Object.entries(this.routes)) {
      const match = path.match(route.regex);
      if (match) {
        const params = {};
        route.paramNames.forEach((name, i) => params[name] = match[i + 1]);
        route.handler(params);
        return;
      }
    }
    // 404
    if (this.routes['*']) this.routes['*'].handler();
  }
}

// Usage
const router = new Router();
router.addRoute('/', () => console.log('Home'));
router.addRoute('/users/:id', ({ id }) => console.log(`User ${id}`));
router.addRoute('*', () => console.log('404'));
router.navigate(location.pathname);
```
</details>

<details>
<summary><b>Implement a mini Redux store with subscribe, dispatch, reducer</b></summary>

```javascript
function createStore(reducer, initialState) {
  let state = initialState;
  let listeners = [];

  return {
    getState() {
      return state;
    },

    dispatch(action) {
      state = reducer(state, action);
      listeners.forEach(listener => listener());
      return action;
    },

    subscribe(listener) {
      listeners.push(listener);
      // Return unsubscribe function
      return () => {
        listeners = listeners.filter(l => l !== listener);
      };
    }
  };
}

// Usage
const reducer = (state = { count: 0 }, action) => {
  switch (action.type) {
    case 'INCREMENT': return { ...state, count: state.count + 1 };
    case 'DECREMENT': return { ...state, count: state.count - 1 };
    default: return state;
  }
};

const store = createStore(reducer, { count: 0 });
const unsubscribe = store.subscribe(() => console.log(store.getState()));
store.dispatch({ type: 'INCREMENT' }); // { count: 1 }
```
</details>

<details>
<summary><b>Write a diff algorithm to compare two JSON objects</b></summary>

```javascript
function diff(oldObj, newObj, path = '') {
  const changes = [];
  const allKeys = new Set([...Object.keys(oldObj || {}), ...Object.keys(newObj || {})]);

  for (const key of allKeys) {
    const currentPath = path ? `${path}.${key}` : key;
    const oldVal = oldObj?.[key];
    const newVal = newObj?.[key];

    if (!(key in (newObj || {}))) {
      changes.push({ type: 'DELETED', path: currentPath, oldValue: oldVal });
    } else if (!(key in (oldObj || {}))) {
      changes.push({ type: 'ADDED', path: currentPath, newValue: newVal });
    } else if (typeof oldVal === 'object' && typeof newVal === 'object' &&
               oldVal !== null && newVal !== null) {
      changes.push(...diff(oldVal, newVal, currentPath));
    } else if (oldVal !== newVal) {
      changes.push({ type: 'CHANGED', path: currentPath, oldValue: oldVal, newValue: newVal });
    }
  }

  return changes;
}

// Usage
const old = { a: 1, b: { c: 2 }, d: 3 };
const current = { a: 1, b: { c: 5 }, e: 4 };
console.log(diff(old, current));
// [{ type: 'CHANGED', path: 'b.c', oldValue: 2, newValue: 5 },
//  { type: 'DELETED', path: 'd', oldValue: 3 },
//  { type: 'ADDED', path: 'e', newValue: 4 }]
```
</details>

<details>
<summary><b>Implement async memoization that handles parallel requests</b></summary>

Async memoization caches results of async functions and handles concurrent calls correctly:

```javascript
function memoizeAsync(fn) {
  const cache = new Map();
  const pending = new Map();

  return function(...args) {
    const key = JSON.stringify(args);

    // Return cached result
    if (cache.has(key)) {
      return Promise.resolve(cache.get(key));
    }

    // Return pending promise if request in flight
    if (pending.has(key)) {
      return pending.get(key);
    }

    // Execute new request
    const promise = fn.apply(this, args)
      .then(result => {
        cache.set(key, result);
        pending.delete(key);
        return result;
      })
      .catch(error => {
        pending.delete(key);
        throw error;
      });

    pending.set(key, promise);
    return promise;
  };
}

// Usage
const memoizedFetch = memoizeAsync(async (userId) => {
  const res = await fetch(`/api/users/${userId}`);
  return res.json();
});

// These will share the same request (deduplication)
memoizedFetch(1); // Makes request
memoizedFetch(1); // Returns same pending promise
memoizedFetch(1); // Returns same pending promise
```

**Key features:**
- Caches successful results
- Deduplicates parallel requests with same args
- Removes pending state on error (allows retry)
- Uses JSON.stringify for deep key comparison
</details>

<details>
<summary><b>Implement search-as-you-type with caching + debounce</b></summary>

```javascript
function createSearchHandler(searchFn, debounceMs = 300) {
  const cache = new Map();
  let timeoutId;
  let abortController;

  return async function search(query, onResults) {
    // Clear previous timeout
    clearTimeout(timeoutId);

    // Abort previous request
    abortController?.abort();

    if (!query.trim()) {
      onResults([]);
      return;
    }

    // Check cache
    if (cache.has(query)) {
      onResults(cache.get(query));
      return;
    }

    // Debounce
    timeoutId = setTimeout(async () => {
      abortController = new AbortController();

      try {
        const results = await searchFn(query, abortController.signal);
        cache.set(query, results);
        onResults(results);
      } catch (err) {
        if (err.name !== 'AbortError') console.error(err);
      }
    }, debounceMs);
  };
}

// Usage
const handleSearch = createSearchHandler(
  async (query, signal) => {
    const res = await fetch(`/api/search?q=${query}`, { signal });
    return res.json();
  }
);

input.addEventListener('input', (e) => {
  handleSearch(e.target.value, (results) => {
    renderResults(results);
  });
});
```
</details>
