# TypeScript Interview Questions

## Basic Types & Variable Declarations

<details>
<summary><b>What are type assertions in TypeScript?</b></summary>

Type assertions tell compiler "trust me, I know the type". Two syntaxes: `value as Type` or `<Type>value`. Used when you know more about the type than TypeScript can infer. Example: `const input = document.getElementById('input') as HTMLInputElement`.
</details>

<details>
<summary><b>What is the difference between union and intersection types?</b></summary>

- **Union** (`A | B`): Value can be A OR B. Example: `string | number` - can be either string or number
- **Intersection** (`A & B`): Value must be A AND B combined. Example: `Person & Employee` - has all properties from both types
</details>

## Interfaces

<details>
<summary><b>What are Interfaces in TypeScript?</b></summary>

Interfaces define the shape/structure of an object. They describe what properties and methods an object should have. Used for type checking. Can be extended and implemented by classes. Example: `interface User { name: string; age: number; }`.
</details>

<details>
<summary><b>What does the 'Omit' type do?</b></summary>

Omit creates new type by removing specified properties from existing type. Example: `type UserWithoutPassword = Omit<User, 'password'>` - creates User type without password property.
</details>

<details>
<summary><b>How to easily make all properties of an interface optional?</b></summary>

Use `Partial<T>` utility type. Example: `type OptionalUser = Partial<User>` - all properties become optional (with `?`).
</details>

<details>
<summary><b>How do you create a new type using a subset of an interface?</b></summary>

Use `Pick<T, Keys>` utility type. Example: `type UserBasic = Pick<User, 'name' | 'email'>` - only includes name and email properties.
</details>

## Classes

<details>
<summary><b>What are Classes in TypeScript? List out some of the features.</b></summary>

Classes are blueprints for objects. Features:
- Access modifiers: `public`, `private`, `protected`
- `readonly` properties
- Static members
- Abstract classes and methods
- Getters/setters
- Implements interfaces
- Extends other classes
</details>

<details>
<summary><b>What is the difference between extends and implements in TypeScript?</b></summary>

- **extends**: Inherit from a class. Get parent's implementation. Single inheritance only
- **implements**: Promise to follow interface contract. Must implement all methods yourself. Can implement multiple interfaces
</details>

## Enums

<details>
<summary><b>What are Enums in TypeScript?</b></summary>

Enums define named constants. Numeric enums (default, start from 0) or string enums. Example:
```typescript
enum Status { Pending, Active, Done } // 0, 1, 2
enum Color { Red = 'RED', Blue = 'BLUE' } // string enum
```
Use for fixed set of related values like status codes, directions, etc.
</details>

<details>
<summary><b>What is the difference between enum, const enum, and union types?</b></summary>

**Regular enum** - exists at runtime:
```typescript
enum Status { Pending, Approved, Rejected }
// Compiles to JavaScript object
```
- Supports reverse mapping (numeric only)
- Adds runtime code

**const enum** - inlined at compile time:
```typescript
const enum Role { Admin, User }
// Values inlined directly, no runtime object
```
- Better performance (no lookup)
- Cannot iterate over values

**Union of literals** - no runtime overhead:
```typescript
type Status = 'pending' | 'approved' | 'rejected';
```
- Type-only, erased at compile time
- Often preferred in modern TypeScript

| Feature | enum | const enum | Union |
|---------|------|------------|-------|
| Runtime code | Yes | No (inlined) | No |
| Reverse mapping | Yes (numeric) | No | No |
| Iteration | Yes | No | No |
| Tree-shaking | Poor | Good | Good |

**Best practices:**
- Use **union types** when possible (simpler, no runtime cost)
- Use **const enum** for performance-critical numeric constants
- Use **regular enum** only when you need runtime access or reverse mapping

**Interview one-liner:** Prefer union string literals for type safety without runtime overhead; use const enum for performance-critical cases; regular enums add runtime code but support iteration and reverse mapping.
</details>

## Generics

<details>
<summary><b>What are generics and how to use them in TypeScript?</b></summary>

Generics allow creating reusable components that work with multiple types while keeping type safety. Use `<T>` placeholder. Example:
```typescript
function identity<T>(value: T): T { return value; }
identity<string>('hello'); // works with string
identity<number>(42); // works with number
```
</details>

<details>
<summary><b>Explain generics in TypeScript</b></summary>

Generics are type variables. Instead of specifying concrete type, use placeholder that gets filled in when used. Benefits: reusable code, type safety, avoid `any`. Common use: arrays (`Array<T>`), Promises (`Promise<T>`), React components (`FC<Props>`).
</details>

<details>
<summary><b>What are Generic Constraints (extends)?</b></summary>

Constraints limit which types can be used with generics using `extends`:

```typescript
function getLength<T extends { length: number }>(value: T): number {
  return value.length;
}

getLength('hello'); // works - string has length
getLength([1, 2, 3]); // works - array has length
getLength(123); // error - number has no length
```

Constrains acceptable types to those matching the specified shape.
</details>

<details>
<summary><b>How do you use multiple type parameters in generics?</b></summary>

Use comma-separated type parameters for multiple generic types:

```typescript
function map<K, V>(key: K, value: V): [K, V] {
  return [key, value];
}

map<string, number>('age', 25); // [string, number]
```

Common in: Map/Dictionary types, key-value operations, tuple creation.
</details>

<details>
<summary><b>What are default generic types?</b></summary>

Provide default type when none is specified:

```typescript
interface Result<T = string> {
  data: T;
}

const r1: Result = { data: 'hello' }; // T defaults to string
const r2: Result<number> = { data: 42 }; // T is number
```

Useful for: optional type parameters, backward compatibility, common use cases.
</details>

<details>
<summary><b>What is the difference between `any` and generics?</b></summary>

| Feature | `any` | Generics |
|---------|-------|----------|
| Type checking | None | Full typing |
| Errors | Runtime | Compile-time |
| Type preservation | Lost | Preserved |

`any` disables type checking. Generics preserve type information while allowing flexibility.
</details>

## Union Types

<details>
<summary><b>Union Types - explain and demonstrate</b></summary>

Union type allows variable to be one of several types. Use `|` operator. Example:
```typescript
let id: string | number;
id = '123'; // valid
id = 123; // valid
id = true; // error
```
TypeScript narrows type in conditionals (type guards).
</details>

<details>
<summary><b>What are Discriminated Unions (Tagged Unions)?</b></summary>

Discriminated unions use a common property (discriminant) to narrow types. Essential pattern for handling different states safely.

```typescript
type Success = { type: 'success'; data: string };
type Error = { type: 'error'; message: string };
type Loading = { type: 'loading' };

type Result = Success | Error | Loading;

function handle(result: Result) {
  switch (result.type) {
    case 'success':
      console.log(result.data); // TypeScript knows it's Success
      break;
    case 'error':
      console.log(result.message); // TypeScript knows it's Error
      break;
    case 'loading':
      console.log('Loading...');
      break;
  }
}
```

Benefits: exhaustive checking, type-safe access to properties, cleaner than type assertions. Common uses: API responses, state management, event handling.
</details>

<details>
<summary><b>What is Type Narrowing and how does it work?</b></summary>

TypeScript automatically narrows union types based on control flow analysis:

```typescript
function printId(id: string | number) {
  if (typeof id === 'string') {
    console.log(id.toUpperCase()); // id is string here
  } else {
    console.log(id.toFixed(2)); // id is number here
  }
}
```

Narrowing methods:
- `typeof` for primitives
- `instanceof` for classes
- `in` operator for properties
- Discriminated unions (common property check)
- Custom type guards (`value is Type`)
</details>

## Unknown Keyword

<details>
<summary><b>When to use the 'unknown' keyword?</b></summary>

Use `unknown` when you don't know the type in advance. Safer than `any` - forces you to check type before using. Good for API responses, user input. Example:
```typescript
let data: unknown = fetchData();
if (typeof data === 'string') {
  console.log(data.toUpperCase()); // safe, type narrowed
}
```
</details>

## Utility Types

<details>
<summary><b>Describe common utility types (Partial, Required, Pick, Omit, etc.)</b></summary>

- `Partial<T>`: All properties optional
- `Required<T>`: All properties required
- `Pick<T, K>`: Select specific properties
- `Omit<T, K>`: Exclude specific properties
- `Readonly<T>`: All properties readonly
- `Record<K, V>`: Object with keys K and values V
- `ReturnType<T>`: Get function return type
- `Parameters<T>`: Get function parameter types as tuple
</details>

## Type Safety

<details>
<summary><b>What are TypeScript Safeguards?</b></summary>

TypeScript adds type checking before code runs (compile time). It helps catch errors early during development - typos, wrong arguments, missing properties. This makes large applications safer and easier to maintain. Safeguards include: type guards (`typeof`, `instanceof`, custom), narrowing, discriminated unions, `never` type for exhaustive checks.
</details>

## Advanced Type System

<details>
<summary><b>How does TypeScript compile-time type narrowing work?</b></summary>

Type narrowing is TypeScript's ability to refine types based on control flow analysis. The compiler tracks type information through code paths.

**Narrowing techniques:**

1. **typeof guards:**
```typescript
function process(value: string | number) {
  if (typeof value === 'string') {
    // TypeScript knows value is string here
    return value.toUpperCase();
  }
  // TypeScript knows value is number here
  return value.toFixed(2);
}
```

2. **Truthiness narrowing:**
```typescript
function printName(name: string | null | undefined) {
  if (name) {
    // name is string (not null/undefined)
    console.log(name.toUpperCase());
  }
}
```

3. **instanceof narrowing:**
```typescript
function logDate(x: Date | string) {
  if (x instanceof Date) {
    console.log(x.toUTCString()); // x is Date
  } else {
    console.log(x.toUpperCase()); // x is string
  }
}
```

4. **in operator narrowing:**
```typescript
type Fish = { swim: () => void };
type Bird = { fly: () => void };

function move(animal: Fish | Bird) {
  if ('swim' in animal) {
    animal.swim(); // animal is Fish
  } else {
    animal.fly(); // animal is Bird
  }
}
```

5. **Custom type guards:**
```typescript
function isString(value: unknown): value is string {
  return typeof value === 'string';
}

function process(value: unknown) {
  if (isString(value)) {
    // TypeScript knows value is string
    console.log(value.toUpperCase());
  }
}
```

6. **Discriminated unions:**
```typescript
type Result =
  | { status: 'success'; data: string }
  | { status: 'error'; error: Error };

function handle(result: Result) {
  if (result.status === 'success') {
    console.log(result.data); // TypeScript knows data exists
  } else {
    console.log(result.error); // TypeScript knows error exists
  }
}
```

**Control flow analysis** means TypeScript tracks assignments:
```typescript
let x: string | number = Math.random() > 0.5 ? 'hello' : 42;
// x is string | number

x = 'definitely a string';
// x is now string (narrowed by assignment)
```
</details>

<details>
<summary><b>Write complex utility types (Partial, Required, Pick, Omit, Record) from scratch</b></summary>

```typescript
// Partial<T> - makes all properties optional
type MyPartial<T> = {
  [P in keyof T]?: T[P];
};

// Required<T> - makes all properties required
type MyRequired<T> = {
  [P in keyof T]-?: T[P];  // -? removes optional modifier
};

// Readonly<T> - makes all properties readonly
type MyReadonly<T> = {
  readonly [P in keyof T]: T[P];
};

// Pick<T, K> - select specific properties
type MyPick<T, K extends keyof T> = {
  [P in K]: T[P];
};

// Omit<T, K> - exclude specific properties
type MyOmit<T, K extends keyof any> = {
  [P in Exclude<keyof T, K>]: T[P];
};
// Or using Pick:
type MyOmit2<T, K extends keyof any> = Pick<T, Exclude<keyof T, K>>;

// Record<K, V> - create object type with keys K and values V
type MyRecord<K extends keyof any, V> = {
  [P in K]: V;
};

// Exclude<T, U> - remove types from T that are assignable to U
type MyExclude<T, U> = T extends U ? never : T;

// Extract<T, U> - extract types from T that are assignable to U
type MyExtract<T, U> = T extends U ? T : never;

// NonNullable<T> - remove null and undefined
type MyNonNullable<T> = T extends null | undefined ? never : T;

// ReturnType<T> - get function return type
type MyReturnType<T extends (...args: any) => any> =
  T extends (...args: any) => infer R ? R : any;

// Parameters<T> - get function parameter types as tuple
type MyParameters<T extends (...args: any) => any> =
  T extends (...args: infer P) => any ? P : never;

// Awaited<T> - unwrap Promise type
type MyAwaited<T> = T extends Promise<infer U> ? MyAwaited<U> : T;

// DeepPartial - recursive partial
type DeepPartial<T> = {
  [P in keyof T]?: T[P] extends object ? DeepPartial<T[P]> : T[P];
};

// Usage examples
interface User {
  id: number;
  name: string;
  email: string;
  address: {
    city: string;
    country: string;
  };
}

type PartialUser = MyPartial<User>;
// { id?: number; name?: string; email?: string; address?: {...} }

type UserPreview = MyPick<User, 'id' | 'name'>;
// { id: number; name: string }

type UserWithoutEmail = MyOmit<User, 'email'>;
// { id: number; name: string; address: {...} }

type StringRecord = MyRecord<'a' | 'b', string>;
// { a: string; b: string }
```
</details>

<details>
<summary><b>What are conditional types and how to use them?</b></summary>

Conditional types select types based on conditions, similar to ternary operator for types.

**Syntax:** `T extends U ? X : Y`

```typescript
// Basic conditional type
type IsString<T> = T extends string ? true : false;

type A = IsString<string>;  // true
type B = IsString<number>;  // false

// Distributive conditional types (distributes over union)
type ToArray<T> = T extends any ? T[] : never;
type StrOrNumArray = ToArray<string | number>;
// string[] | number[] (not (string | number)[])

// Prevent distribution with tuple
type ToArrayNonDist<T> = [T] extends [any] ? T[] : never;
type Mixed = ToArrayNonDist<string | number>;
// (string | number)[]

// infer keyword - extract types
type GetReturnType<T> = T extends (...args: any[]) => infer R ? R : never;
type Num = GetReturnType<() => number>;  // number

// Extract array element type
type ElementType<T> = T extends (infer U)[] ? U : T;
type El = ElementType<string[]>;  // string

// Nested inference
type UnwrapPromise<T> = T extends Promise<infer U>
  ? UnwrapPromise<U>  // Recursive for nested promises
  : T;

type Unwrapped = UnwrapPromise<Promise<Promise<string>>>;  // string

// Practical example: function overload types
type Flatten<T> = T extends Array<infer Item> ? Item : T;

function flatten<T>(arr: T[]): Flatten<T>[] {
  return arr.flat() as Flatten<T>[];
}
```
</details>

<details>
<summary><b>What are template literal types?</b></summary>

Template literal types build string types using template literal syntax.

```typescript
// Basic template literal types
type Greeting = `Hello, ${string}`;
const g1: Greeting = 'Hello, World';  // OK
const g2: Greeting = 'Hi, World';     // Error

// Union distribution
type Color = 'red' | 'blue';
type Size = 'small' | 'large';
type ColoredSize = `${Color}-${Size}`;
// 'red-small' | 'red-large' | 'blue-small' | 'blue-large'

// Event handler types
type EventName<T extends string> = `on${Capitalize<T>}`;
type ClickHandler = EventName<'click'>;  // 'onClick'

// Build getter/setter types
type Getters<T> = {
  [K in keyof T as `get${Capitalize<string & K>}`]: () => T[K];
};

interface Person { name: string; age: number; }
type PersonGetters = Getters<Person>;
// { getName: () => string; getAge: () => number; }

// Remove prefix from string literal type
type RemovePrefix<S extends string, P extends string> =
  S extends `${P}${infer Rest}` ? Rest : S;

type Unprefixed = RemovePrefix<'onClick', 'on'>;  // 'Click'

// CSS unit types
type CSSUnit = 'px' | 'em' | 'rem' | '%';
type CSSValue = `${number}${CSSUnit}`;
const width: CSSValue = '100px';   // OK
const height: CSSValue = '10rem';  // OK
```
</details>

## TypeScript with React

<details>
<summary><b>How do you type React components?</b></summary>

```typescript
// Function component with props
type Props = { name: string; count?: number };
const MyComponent = ({ name, count = 0 }: Props) => <div>{name}: {count}</div>;

// Or with React.FC (less recommended now)
const MyComponent: React.FC<Props> = ({ name }) => <div>{name}</div>;
```
Prefer typing props directly over React.FC. FC adds implicit children prop (removed in React 18).
</details>

<details>
<summary><b>What's the difference between FC and function components?</b></summary>

`React.FC<Props>`:
- Implicit children prop (React 17, removed in 18)
- Cannot use generics easily
- Types return automatically

Direct typing:
- Explicit about props
- Better generic support
- More flexible

Modern recommendation: type props directly, avoid FC.
</details>

<details>
<summary><b>How do you type children props?</b></summary>

```typescript
// React.ReactNode for flexible children
type Props = { children: React.ReactNode };

// React.ReactElement for single element
type Props = { children: React.ReactElement };

// Specific types
type Props = { children: string | number };

// Function as children (render props)
type Props = { children: (data: Data) => React.ReactNode };
```
</details>

<details>
<summary><b>How do you type event handlers?</b></summary>

```typescript
// Mouse event
const handleClick = (e: React.MouseEvent<HTMLButtonElement>) => {};

// Change event
const handleChange = (e: React.ChangeEvent<HTMLInputElement>) => {
  console.log(e.target.value);
};

// Form submit
const handleSubmit = (e: React.FormEvent<HTMLFormElement>) => {
  e.preventDefault();
};

// Keyboard event
const handleKeyDown = (e: React.KeyboardEvent<HTMLInputElement>) => {};
```
</details>

<details>
<summary><b>How do you handle generic components in TypeScript?</b></summary>

```typescript
// Generic list component
type ListProps<T> = {
  items: T[];
  renderItem: (item: T) => React.ReactNode;
};

function List<T>({ items, renderItem }: ListProps<T>) {
  return <ul>{items.map(renderItem)}</ul>;
}

// Usage - type is inferred
<List items={users} renderItem={(user) => <li>{user.name}</li>} />
```
</details>

<details>
<summary><b>How do you type custom hooks?</b></summary>

```typescript
// Return tuple
function useToggle(initial: boolean): [boolean, () => void] {
  const [value, setValue] = useState(initial);
  const toggle = useCallback(() => setValue(v => !v), []);
  return [value, toggle];
}

// Return object
function useFetch<T>(url: string): { data: T | null; loading: boolean; error: Error | null } {
  // implementation
}

// With generics
function useLocalStorage<T>(key: string, initial: T): [T, (value: T) => void] {
  // implementation
}
```
</details>

<details>
<summary><b>What's the difference between type and interface?</b></summary>

Both define object shapes, but:

**Interface:**
- Can be extended/merged (declaration merging)
- Better for public APIs
- Only for object types

**Type:**
- Can represent unions, tuples, primitives
- Cannot be merged
- More flexible

```typescript
// Interface merging
interface User { name: string }
interface User { age: number }
// User has both name and age

// Type union (not possible with interface)
type Status = 'pending' | 'done' | 'error';
```

Use interface for objects that may be extended, type for unions and complex types.
</details>
