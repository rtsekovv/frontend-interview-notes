# Вопросы для собеседования по TypeScript

## Базовые типы и объявление переменных

<details>
<summary><b>Что такое type assertions в TypeScript?</b></summary>

Type assertions говорят компилятору "доверься мне, я знаю тип". Два синтаксиса: `value as Type` или `<Type>value`. Используется когда вы знаете о типе больше, чем TypeScript может вывести. Пример: `const input = document.getElementById('input') as HTMLInputElement`.
</details>

<details>
<summary><b>В чём разница между union и intersection типами?</b></summary>

- **Union** (`A | B`): Значение может быть A ИЛИ B. Пример: `string | number` — может быть либо string, либо number
- **Intersection** (`A & B`): Значение должно быть A И B вместе. Пример: `Person & Employee` — имеет все свойства обоих типов
</details>

## Interfaces

<details>
<summary><b>Что такое Interfaces в TypeScript?</b></summary>

Interfaces определяют форму/структуру объекта. Они описывают какие свойства и методы должен иметь объект. Используются для проверки типов. Могут расширяться и реализовываться классами. Пример: `interface User { name: string; age: number; }`.
</details>

<details>
<summary><b>Что делает тип 'Omit'?</b></summary>

Omit создаёт новый тип, удаляя указанные свойства из существующего типа. Пример: `type UserWithoutPassword = Omit<User, 'password'>` — создаёт тип User без свойства password.
</details>

<details>
<summary><b>Как легко сделать все свойства interface опциональными?</b></summary>

Используйте utility type `Partial<T>`. Пример: `type OptionalUser = Partial<User>` — все свойства становятся опциональными (с `?`).
</details>

<details>
<summary><b>Как создать новый тип, используя подмножество interface?</b></summary>

Используйте utility type `Pick<T, Keys>`. Пример: `type UserBasic = Pick<User, 'name' | 'email'>` — включает только свойства name и email.
</details>

## Classes

<details>
<summary><b>Что такое Classes в TypeScript? Перечислите некоторые фичи.</b></summary>

Classes — это blueprints для объектов. Фичи:
- Модификаторы доступа: `public`, `private`, `protected`
- Свойства `readonly`
- Static members
- Abstract classes и methods
- Getters/setters
- Implements interfaces
- Extends другие классы
</details>

<details>
<summary><b>В чём разница между extends и implements в TypeScript?</b></summary>

- **extends**: Наследование от класса. Получаете реализацию родителя. Только одиночное наследование
- **implements**: Обещание следовать контракту interface. Нужно реализовать все методы самостоятельно. Можно implements несколько interfaces
</details>

## Enums

<details>
<summary><b>Что такое Enums в TypeScript?</b></summary>

Enums определяют именованные константы. Numeric enums (по умолчанию, начиная с 0) или string enums. Пример:
```typescript
enum Status { Pending, Active, Done } // 0, 1, 2
enum Color { Red = 'RED', Blue = 'BLUE' } // string enum
```
Используйте для фиксированного набора связанных значений типа status codes, directions и т.д.
</details>

<details>
<summary><b>В чём разница между enum, const enum и union types?</b></summary>

**Обычный enum** — существует в runtime:
```typescript
enum Status { Pending, Approved, Rejected }
// Компилируется в JavaScript-объект
```
- Поддерживает reverse mapping (только для numeric)
- Добавляет runtime-код

**const enum** — инлайнится во время компиляции:
```typescript
const enum Role { Admin, User }
// Значения инлайнятся напрямую, нет runtime-объекта
```
- Лучшая производительность (нет lookup)
- Нельзя итерировать по значениям

**Union литералов** — нет runtime overhead:
```typescript
type Status = 'pending' | 'approved' | 'rejected';
```
- Только type-level, стирается при компиляции
- Часто предпочтительнее в современном TypeScript

| Фича | enum | const enum | Union |
|------|------|------------|-------|
| Runtime-код | Да | Нет (inlined) | Нет |
| Reverse mapping | Да (numeric) | Нет | Нет |
| Итерация | Да | Нет | Нет |
| Tree-shaking | Плохо | Хорошо | Хорошо |

**Лучшие практики:**
- Используйте **union types** когда возможно (проще, без runtime cost)
- Используйте **const enum** для performance-critical numeric констант
- Используйте **обычный enum** только когда нужен runtime-доступ или reverse mapping

**Ответ для собеседования:** Предпочитайте union string literals для типобезопасности без runtime overhead; используйте const enum для performance-critical случаев; обычные enums добавляют runtime-код, но поддерживают итерацию и reverse mapping.
</details>

## Generics

<details>
<summary><b>Что такое generics и как их использовать в TypeScript?</b></summary>

Generics позволяют создавать переиспользуемые компоненты, работающие с разными типами, сохраняя типобезопасность. Используйте placeholder `<T>`. Пример:
```typescript
function identity<T>(value: T): T { return value; }
identity<string>('hello'); // работает со string
identity<number>(42); // работает с number
```
</details>

<details>
<summary><b>Объясните generics в TypeScript</b></summary>

Generics — это переменные типов. Вместо указания конкретного типа используется placeholder, который заполняется при использовании. Преимущества: переиспользуемый код, типобезопасность, избежание `any`. Распространённое использование: массивы (`Array<T>`), Promises (`Promise<T>`), React-компоненты (`FC<Props>`).
</details>

<details>
<summary><b>Что такое Generic Constraints (extends)?</b></summary>

Constraints ограничивают какие типы можно использовать с generics через `extends`:

```typescript
function getLength<T extends { length: number }>(value: T): number {
  return value.length;
}

getLength('hello'); // работает — string имеет length
getLength([1, 2, 3]); // работает — array имеет length
getLength(123); // ошибка — number не имеет length
```

Ограничивает допустимые типы теми, которые соответствуют указанной форме.
</details>

<details>
<summary><b>Как использовать несколько type parameters в generics?</b></summary>

Используйте type parameters, разделённые запятыми:

```typescript
function map<K, V>(key: K, value: V): [K, V] {
  return [key, value];
}

map<string, number>('age', 25); // [string, number]
```

Распространено в: Map/Dictionary types, key-value операциях, создании tuples.
</details>

<details>
<summary><b>Что такое default generic types?</b></summary>

Предоставляют тип по умолчанию, когда никакой не указан:

```typescript
interface Result<T = string> {
  data: T;
}

const r1: Result = { data: 'hello' }; // T по умолчанию string
const r2: Result<number> = { data: 42 }; // T это number
```

Полезно для: опциональных type parameters, обратной совместимости, распространённых случаев использования.
</details>

<details>
<summary><b>В чём разница между `any` и generics?</b></summary>

| Фича | `any` | Generics |
|------|-------|----------|
| Проверка типов | Нет | Полная типизация |
| Ошибки | Runtime | Compile-time |
| Сохранение типа | Теряется | Сохраняется |

`any` отключает проверку типов. Generics сохраняют информацию о типе, обеспечивая гибкость.
</details>

## Union Types

<details>
<summary><b>Union Types — объясните и продемонстрируйте</b></summary>

Union type позволяет переменной быть одним из нескольких типов. Используйте оператор `|`. Пример:
```typescript
let id: string | number;
id = '123'; // валидно
id = 123; // валидно
id = true; // ошибка
```
TypeScript сужает тип в условиях (type guards).
</details>

<details>
<summary><b>Что такое Discriminated Unions (Tagged Unions)?</b></summary>

Discriminated unions используют общее свойство (discriminant) для сужения типов. Важный паттерн для безопасной обработки разных состояний.

```typescript
type Success = { type: 'success'; data: string };
type Error = { type: 'error'; message: string };
type Loading = { type: 'loading' };

type Result = Success | Error | Loading;

function handle(result: Result) {
  switch (result.type) {
    case 'success':
      console.log(result.data); // TypeScript знает, что это Success
      break;
    case 'error':
      console.log(result.message); // TypeScript знает, что это Error
      break;
    case 'loading':
      console.log('Loading...');
      break;
  }
}
```

Преимущества: exhaustive checking, типобезопасный доступ к свойствам, чище чем type assertions. Распространённые применения: API responses, state management, event handling.
</details>

<details>
<summary><b>Что такое Type Narrowing и как это работает?</b></summary>

TypeScript автоматически сужает union types на основе анализа control flow:

```typescript
function printId(id: string | number) {
  if (typeof id === 'string') {
    console.log(id.toUpperCase()); // id здесь string
  } else {
    console.log(id.toFixed(2)); // id здесь number
  }
}
```

Методы сужения:
- `typeof` для примитивов
- `instanceof` для классов
- Оператор `in` для свойств
- Discriminated unions (проверка общего свойства)
- Custom type guards (`value is Type`)
</details>

## Unknown Keyword

<details>
<summary><b>Когда использовать ключевое слово 'unknown'?</b></summary>

Используйте `unknown` когда не знаете тип заранее. Безопаснее, чем `any` — заставляет проверять тип перед использованием. Хорош для API responses, пользовательского ввода. Пример:
```typescript
let data: unknown = fetchData();
if (typeof data === 'string') {
  console.log(data.toUpperCase()); // безопасно, тип сужен
}
```
</details>

## Utility Types

<details>
<summary><b>Опишите распространённые utility types (Partial, Required, Pick, Omit и т.д.)</b></summary>

- `Partial<T>`: Все свойства опциональны
- `Required<T>`: Все свойства обязательны
- `Pick<T, K>`: Выбрать определённые свойства
- `Omit<T, K>`: Исключить определённые свойства
- `Readonly<T>`: Все свойства readonly
- `Record<K, V>`: Объект с ключами K и значениями V
- `ReturnType<T>`: Получить return type функции
- `Parameters<T>`: Получить типы параметров функции как tuple
</details>

## Type Safety

<details>
<summary><b>Что такое TypeScript Safeguards?</b></summary>

TypeScript добавляет проверку типов до запуска кода (compile time). Помогает ловить ошибки рано в процессе разработки — опечатки, неправильные аргументы, отсутствующие свойства. Это делает большие приложения безопаснее и проще в поддержке. Safeguards включают: type guards (`typeof`, `instanceof`, custom), narrowing, discriminated unions, тип `never` для exhaustive checks.
</details>

## Продвинутая система типов

<details>
<summary><b>Как работает compile-time type narrowing в TypeScript?</b></summary>

Type narrowing — это способность TypeScript уточнять типы на основе анализа control flow. Компилятор отслеживает информацию о типах через пути выполнения кода.

**Техники сужения:**

1. **typeof guards:**
```typescript
function process(value: string | number) {
  if (typeof value === 'string') {
    // TypeScript знает, что value это string здесь
    return value.toUpperCase();
  }
  // TypeScript знает, что value это number здесь
  return value.toFixed(2);
}
```

2. **Сужение по truthiness:**
```typescript
function printName(name: string | null | undefined) {
  if (name) {
    // name это string (не null/undefined)
    console.log(name.toUpperCase());
  }
}
```

3. **instanceof сужение:**
```typescript
function logDate(x: Date | string) {
  if (x instanceof Date) {
    console.log(x.toUTCString()); // x это Date
  } else {
    console.log(x.toUpperCase()); // x это string
  }
}
```

4. **Сужение через оператор in:**
```typescript
type Fish = { swim: () => void };
type Bird = { fly: () => void };

function move(animal: Fish | Bird) {
  if ('swim' in animal) {
    animal.swim(); // animal это Fish
  } else {
    animal.fly(); // animal это Bird
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
    // TypeScript знает, что value это string
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
    console.log(result.data); // TypeScript знает, что data существует
  } else {
    console.log(result.error); // TypeScript знает, что error существует
  }
}
```

**Анализ control flow** означает, что TypeScript отслеживает присваивания:
```typescript
let x: string | number = Math.random() > 0.5 ? 'hello' : 42;
// x это string | number

x = 'definitely a string';
// x теперь string (сужен через присваивание)
```
</details>

<details>
<summary><b>Напишите сложные utility types (Partial, Required, Pick, Omit, Record) с нуля</b></summary>

```typescript
// Partial<T> — делает все свойства опциональными
type MyPartial<T> = {
  [P in keyof T]?: T[P];
};

// Required<T> — делает все свойства обязательными
type MyRequired<T> = {
  [P in keyof T]-?: T[P];  // -? убирает optional modifier
};

// Readonly<T> — делает все свойства readonly
type MyReadonly<T> = {
  readonly [P in keyof T]: T[P];
};

// Pick<T, K> — выбирает определённые свойства
type MyPick<T, K extends keyof T> = {
  [P in K]: T[P];
};

// Omit<T, K> — исключает определённые свойства
type MyOmit<T, K extends keyof any> = {
  [P in Exclude<keyof T, K>]: T[P];
};
// Или через Pick:
type MyOmit2<T, K extends keyof any> = Pick<T, Exclude<keyof T, K>>;

// Record<K, V> — создаёт object type с ключами K и значениями V
type MyRecord<K extends keyof any, V> = {
  [P in K]: V;
};

// Exclude<T, U> — удаляет типы из T, присваиваемые U
type MyExclude<T, U> = T extends U ? never : T;

// Extract<T, U> — извлекает типы из T, присваиваемые U
type MyExtract<T, U> = T extends U ? T : never;

// NonNullable<T> — удаляет null и undefined
type MyNonNullable<T> = T extends null | undefined ? never : T;

// ReturnType<T> — получает return type функции
type MyReturnType<T extends (...args: any) => any> =
  T extends (...args: any) => infer R ? R : any;

// Parameters<T> — получает типы параметров функции как tuple
type MyParameters<T extends (...args: any) => any> =
  T extends (...args: infer P) => any ? P : never;

// Awaited<T> — разворачивает Promise type
type MyAwaited<T> = T extends Promise<infer U> ? MyAwaited<U> : T;

// DeepPartial — рекурсивный partial
type DeepPartial<T> = {
  [P in keyof T]?: T[P] extends object ? DeepPartial<T[P]> : T[P];
};

// Примеры использования
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
<summary><b>Что такое conditional types и как их использовать?</b></summary>

Conditional types выбирают типы на основе условий, аналогично тернарному оператору для типов.

**Синтаксис:** `T extends U ? X : Y`

```typescript
// Базовый conditional type
type IsString<T> = T extends string ? true : false;

type A = IsString<string>;  // true
type B = IsString<number>;  // false

// Distributive conditional types (распределяется по union)
type ToArray<T> = T extends any ? T[] : never;
type StrOrNumArray = ToArray<string | number>;
// string[] | number[] (не (string | number)[])

// Предотвращение distribution через tuple
type ToArrayNonDist<T> = [T] extends [any] ? T[] : never;
type Mixed = ToArrayNonDist<string | number>;
// (string | number)[]

// Ключевое слово infer — извлечение типов
type GetReturnType<T> = T extends (...args: any[]) => infer R ? R : never;
type Num = GetReturnType<() => number>;  // number

// Извлечение типа элемента массива
type ElementType<T> = T extends (infer U)[] ? U : T;
type El = ElementType<string[]>;  // string

// Вложенный inference
type UnwrapPromise<T> = T extends Promise<infer U>
  ? UnwrapPromise<U>  // Рекурсия для вложенных promises
  : T;

type Unwrapped = UnwrapPromise<Promise<Promise<string>>>;  // string

// Практический пример: типы function overload
type Flatten<T> = T extends Array<infer Item> ? Item : T;

function flatten<T>(arr: T[]): Flatten<T>[] {
  return arr.flat() as Flatten<T>[];
}
```
</details>

<details>
<summary><b>Что такое template literal types?</b></summary>

Template literal types строят string types используя синтаксис template literals.

```typescript
// Базовые template literal types
type Greeting = `Hello, ${string}`;
const g1: Greeting = 'Hello, World';  // OK
const g2: Greeting = 'Hi, World';     // Ошибка

// Union distribution
type Color = 'red' | 'blue';
type Size = 'small' | 'large';
type ColoredSize = `${Color}-${Size}`;
// 'red-small' | 'red-large' | 'blue-small' | 'blue-large'

// Типы event handler
type EventName<T extends string> = `on${Capitalize<T>}`;
type ClickHandler = EventName<'click'>;  // 'onClick'

// Построение типов getter/setter
type Getters<T> = {
  [K in keyof T as `get${Capitalize<string & K>}`]: () => T[K];
};

interface Person { name: string; age: number; }
type PersonGetters = Getters<Person>;
// { getName: () => string; getAge: () => number; }

// Удаление префикса из string literal type
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

## TypeScript с React

<details>
<summary><b>Как типизировать React компоненты?</b></summary>

```typescript
// Function component с props
type Props = { name: string; count?: number };
const MyComponent = ({ name, count = 0 }: Props) => <div>{name}: {count}</div>;

// Или с React.FC (сейчас менее рекомендуется)
const MyComponent: React.FC<Props> = ({ name }) => <div>{name}</div>;
```
Предпочитайте типизировать props напрямую вместо React.FC. FC добавляет неявный children prop (убран в React 18).
</details>

<details>
<summary><b>В чём разница между FC и function components?</b></summary>

`React.FC<Props>`:
- Неявный children prop (React 17, убран в 18)
- Сложно использовать generics
- Типизирует return автоматически

Прямая типизация:
- Явно про props
- Лучшая поддержка generic
- Более гибко

Современная рекомендация: типизируйте props напрямую, избегайте FC.
</details>

<details>
<summary><b>Как типизировать children props?</b></summary>

```typescript
// React.ReactNode для гибких children
type Props = { children: React.ReactNode };

// React.ReactElement для одного элемента
type Props = { children: React.ReactElement };

// Специфичные типы
type Props = { children: string | number };

// Function as children (render props)
type Props = { children: (data: Data) => React.ReactNode };
```
</details>

<details>
<summary><b>Как типизировать event handlers?</b></summary>

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
<summary><b>Как работать с generic компонентами в TypeScript?</b></summary>

```typescript
// Generic list component
type ListProps<T> = {
  items: T[];
  renderItem: (item: T) => React.ReactNode;
};

function List<T>({ items, renderItem }: ListProps<T>) {
  return <ul>{items.map(renderItem)}</ul>;
}

// Использование - тип выводится автоматически
<List items={users} renderItem={(user) => <li>{user.name}</li>} />
```
</details>

<details>
<summary><b>Как типизировать custom hooks?</b></summary>

```typescript
// Возврат tuple
function useToggle(initial: boolean): [boolean, () => void] {
  const [value, setValue] = useState(initial);
  const toggle = useCallback(() => setValue(v => !v), []);
  return [value, toggle];
}

// Возврат объекта
function useFetch<T>(url: string): { data: T | null; loading: boolean; error: Error | null } {
  // implementation
}
```
</details>

<details>
<summary><b>В чём разница между type и interface?</b></summary>

Оба определяют форму объекта, но:

**Interface:**
- Можно расширять/сливать (declaration merging)
- Лучше для публичных API
- Только для объектных типов

**Type:**
- Может представлять unions, tuples, примитивы
- Нельзя сливать
- Более гибкий

```typescript
// Interface merging
interface User { name: string }
interface User { age: number }
// User имеет и name, и age

// Type union (невозможно с interface)
type Status = 'pending' | 'done' | 'error';
```

Используйте interface для объектов, которые могут расширяться, type для unions и сложных типов.
</details>
