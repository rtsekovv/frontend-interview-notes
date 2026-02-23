# Вопросы для собеседования по JavaScript

## Scope и Closures

<details>
<summary><b>Что такое temporal dead zone и зачем она нужна?</b></summary>

TDZ — период между входом в scope и объявлением переменной. Переменные с `let`/`const` находятся в TDZ и недоступны. Цель: ловить ошибки рано, предотвращать путаницу когда переменная существует, но undefined. Заставляет писать чище — объявлять до использования.
</details>

<details>
<summary><b>Что происходит с const в цикле for...of?</b></summary>

Работает нормально, потому что каждая итерация создаёт новую привязку. Переменная объявляется заново каждую итерацию, а не переприсваивается:
```javascript
for (const item of [1, 2, 3]) {
  console.log(item); // Работает: 1, 2, 3
}
// Но это не работает:
for (const i = 0; i < 3; i++) { } // Error: Assignment to constant
```
</details>

<details>
<summary><b>Что такое closures и как они работают?</b></summary>

Closure — это функция, которая запоминает переменные из внешней области видимости даже после завершения внешней функции. Внутренняя функция "замыкается" на внешние переменные. Пример:
```javascript
function outer() {
  let count = 0;
  return function inner() { return ++count; };
}
const counter = outer();
counter(); // 1
counter(); // 2 - помнит count
```
</details>

<details>
<summary><b>Объясните различные типы scope в JavaScript</b></summary>

- **Global scope**: Переменные доступны везде
- **Function scope**: Переменные внутри функции, недоступны снаружи
- **Block scope**: Переменные внутри `{}` (только let, const)
- **Lexical scope**: Внутренние функции имеют доступ к переменным внешних функций
</details>

## Hoisting

<details>
<summary><b>Что такое hoisting в JavaScript?</b></summary>

JavaScript перемещает объявления в начало их области видимости перед выполнением. Функции поднимаются полностью. Объявления `var` поднимаются (инициализируются как undefined). `let`/`const` поднимаются, но не инициализируются (temporal dead zone).
</details>

<details>
<summary><b>Чем отличается hoisting для var, let и const?</b></summary>

- `var`: Поднимается и инициализируется как `undefined`. Можно обратиться до объявления (получим undefined)
- `let`/`const`: Поднимаются, но НЕ инициализируются. Обращение до объявления выбрасывает ReferenceError (temporal dead zone)
</details>

## Strict Mode

<details>
<summary><b>Что такое strict mode и зачем его использовать?</b></summary>

`'use strict'` включает более строгий parsing. Преимущества: предотвращает случайные глобальные переменные, выбрасывает ошибки для небезопасных действий, отключает запутывающие фичи. Пример: нельзя использовать необъявленные переменные, нельзя удалять переменные, нельзя дублировать параметры.
</details>

## Reference vs Value

<details>
<summary><b>В чём разница между передачей по ссылке и по значению?</b></summary>

- **По значению**: Примитивы (string, number, boolean). Передаётся копия значения. Изменения не влияют на оригинал
- **По ссылке**: Объекты, массивы. Передаётся ссылка (адрес в памяти). Изменения влияют на оригинальный объект
</details>

## Типы JavaScript

<details>
<summary><b>Какие примитивные типы есть в JavaScript?</b></summary>

7 примитивов: `string`, `number`, `boolean`, `null`, `undefined`, `symbol`, `bigint`. Примитивы иммутабельны и сравниваются по значению.
</details>

<details>
<summary><b>В чём разница между null и undefined?</b></summary>

- `undefined`: Переменная объявлена, но не присвоено значение. Дефолтное возвращаемое значение. Параметр не передан
- `null`: Намеренное отсутствие значения. Явно присвоено разработчиком
- `typeof null === 'object'` (исторический баг)
</details>

<details>
<summary><b>Как работает сравнение в JS? В чём разница между === и Object.is()?</b></summary>

Оба `===` и `Object.is()` проверяют строгое равенство, но отличаются в edge cases:

| Сравнение | `===` | `Object.is()` |
|-----------|-------|---------------|
| `NaN === NaN` | `false` | `true` |
| `+0 === -0` | `true` | `false` |
| Всё остальное | Одинаково | Одинаково |

```javascript
NaN === NaN          // false
Object.is(NaN, NaN)  // true

+0 === -0            // true
Object.is(+0, -0)    // false
```

`Object.is()` — алгоритм "то же значение" — полезен когда нужно математически корректное сравнение. Используется внутри React для сравнения state.
</details>

## let, const и var

<details>
<summary><b>Какие различия между let, const и var?</b></summary>

- `var`: Function scope, hoisting, можно переобъявить, можно переприсвоить
- `let`: Block scope, temporal dead zone, нельзя переобъявить, можно переприсвоить
- `const`: Block scope, temporal dead zone, нельзя переобъявить, нельзя переприсвоить (но свойства объекта можно менять)
</details>

## Functions

<details>
<summary><b>Что такое каррирование функций?</b></summary>

Каррирование преобразует функцию с несколькими аргументами в последовательность функций с одним аргументом. `f(a, b, c)` становится `f(a)(b)(c)`. Полезно для: частичного применения, создания специализированных функций, композиции.
```javascript
const add = a => b => a + b;
const add5 = add(5);
add5(3); // 8
```
</details>

<details>
<summary><b>Что такое частичное применение (partial application)?</b></summary>

Создание новой функции путём предзаполнения некоторых аргументов существующей функции:
```javascript
const multiply = (a, b, c) => a * b * c;
const double = multiply.bind(null, 2, 1); // a=2, b=1 зафиксированы
double(5); // 10
```
</details>

<details>
<summary><b>Что такое функции высшего порядка?</b></summary>

Функции, которые принимают функции как аргументы или возвращают функции. Примеры: `map`, `filter`, `reduce`, `forEach`. Позволяют функциональное программирование, переиспользование кода и абстракцию.
</details>

<details>
<summary><b>Что такое композиция функций?</b></summary>

Комбинирование простых функций для построения сложных. Выход одной функции становится входом следующей:
```javascript
const compose = (f, g) => x => f(g(x));
const addOne = x => x + 1;
const double = x => x * 2;
const addOneThenDouble = compose(double, addOne);
addOneThenDouble(3); // 8
```
</details>

<details>
<summary><b>Как работают параметры по умолчанию?</b></summary>

Устанавливают значение по умолчанию когда аргумент undefined:
```javascript
function greet(name = 'Guest', greeting = 'Hello') {
  return `${greeting}, ${name}`;
}
greet(); // "Hello, Guest"
```
Параметры по умолчанию вычисляются при вызове, слева направо.
</details>

<details>
<summary><b>В чём разница между анонимными и декларативными функциями?</b></summary>

- **Декларативная** (function declaration): Имеет имя, hoisting. `function foo() {}`
- **Анонимная**: Без имени, присваивается переменной или передаётся как callback. `const foo = function() {}`
</details>

<details>
<summary><b>Что такое arrow functions и чем они отличаются от обычных функций?</b></summary>

Arrow functions: короткий синтаксис `() => {}`. Отличия:
- Нет собственного `this` — наследуется от родительского scope
- Нет объекта `arguments`
- Нельзя использовать как конструкторы (нет `new`)
- Нет свойства `prototype`
- Не могут быть генераторами
</details>

## Exception Handling

<details>
<summary><b>Как обрабатывать исключения в JavaScript?</b></summary>

Используйте `try...catch...finally`. `try` содержит рискованный код, `catch` обрабатывает ошибки, `finally` выполняется всегда. Выбрасывайте собственные ошибки через `throw new Error('message')`. Для async: `.catch()` для промисов, try/catch с async/await.
</details>

## Loops

<details>
<summary><b>Какие типы циклов есть в JavaScript?</b></summary>

`for`, `while`, `do...while`, `for...in` (ключи объекта), `for...of` (значения итерируемых), `forEach` (массивы). Используйте `break` для выхода, `continue` для пропуска итерации.
</details>

<details>
<summary><b>В чём разница между for...in и for...of?</b></summary>

- `for...in`: Итерирует по ключам/индексам объекта. Работает с объектами. Может итерировать унаследованные свойства
- `for...of`: Итерирует по значениям. Работает с итерируемыми (массивы, строки, Map, Set). Чище для массивов
</details>

## Context (call, apply, bind)

<details>
<summary><b>Объясните методы call, apply и bind</b></summary>

- `call(thisArg, arg1, arg2)`: Вызов функции с указанным `this`, аргументы передаются по отдельности
- `apply(thisArg, [args])`: То же, что call, но аргументы как массив
- `bind(thisArg, arg1)`: Возвращает новую функцию с постоянно привязанным `this`. Не вызывает сразу
</details>

<details>
<summary><b>Как работает 'this' в JavaScript?</b></summary>

`this` зависит от того, как вызвана функция:
- Вызов метода: `this` = объект перед точкой
- Обычная функция: `this` = global (или undefined в strict mode)
- Arrow function: `this` = унаследован от родительского scope
- Constructor: `this` = новый объект
- Event handler: `this` = элемент, получивший событие
</details>

## Map и Set

<details>
<summary><b>В чём разница между Map и Object?</b></summary>

- **Map**: Любой тип в качестве ключа, сохраняет порядок вставки, есть свойство `size`, итерируемый, лучше для частого добавления/удаления
- **Object**: Только string/symbol ключи, порядок не гарантирован, нужен `Object.keys().length` для размера
</details>

<details>
<summary><b>Когда использовать Set вместо Array?</b></summary>

Используйте Set когда нужны: только уникальные значения, быстрые проверки `has()`, удаление дубликатов из массива (`[...new Set(arr)]`). Set быстрее для операций поиска.
</details>

## Rest и Spread операторы

<details>
<summary><b>Объясните rest и spread операторы</b></summary>

Оба используют `...`, но для разных целей:
- **Spread**: Развернуть массив/объект. `[...arr1, ...arr2]`, `{...obj1, ...obj2}`
- **Rest**: Собрать оставшиеся элементы. `function(a, ...rest)`, `const [first, ...rest] = arr`
</details>

## Promises

<details>
<summary><b>Что такое callback hell и как его избежать?</b></summary>

Глубоко вложенные callbacks, создающие пирамидальный код. Трудно читать, отлаживать, обрабатывать ошибки. Решения: Promises с цепочками `.then()`, синтаксис async/await, разбиение на именованные функции, Promise.all для параллельных операций.
</details>

<details>
<summary><b>В чём разница между Promise.all и Promise.allSettled?</b></summary>

- `Promise.all()`: Резолвится когда ВСЕ промисы резолвятся. Реджектится сразу если ЛЮБОЙ промис реджектится
- `Promise.allSettled()`: Ждёт ВСЕХ промисов до конца (resolve или reject). Возвращает массив со статусом и value/reason для каждого

Используйте `allSettled` когда нужны результаты независимо от отдельных неудач.
</details>

<details>
<summary><b>Когда использовать Promise.race?</b></summary>

Возвращает результат первого завершившегося промиса (resolve или reject). Примеры: паттерны с таймаутом, гонка за самым быстрым ответом:
```javascript
const timeout = new Promise((_, reject) =>
  setTimeout(() => reject('Timeout'), 5000)
);
Promise.race([fetchData(), timeout]);
```
</details>

<details>
<summary><b>Чем Promise.any отличается от Promise.race?</b></summary>

- `Promise.race()`: Завершается с первым завершившимся промисом (resolve ИЛИ reject)
- `Promise.any()`: Резолвится с первым УСПЕШНЫМ промисом. Реджектится только если ВСЕ промисы реджектятся (AggregateError)

Используйте `any` когда нужен первый успешный результат, игнорируя неудачи.
</details>

<details>
<summary><b>Можно ли использовать await вне async функций?</b></summary>

Да, в ES-модулях (top-level await). Работает в `.mjs` файлах или с `"type": "module"` в package.json:
```javascript
// module.mjs
const data = await fetch('/api').then(r => r.json());
export { data };
```
Недоступно в CommonJS или обычных скриптах.
</details>

<details>
<summary><b>Что происходит если не await async функцию?</b></summary>

Возвращает Promise немедленно. Функция выполняется в фоне. Ошибки могут остаться необработанными. Используйте когда не нужен результат, но всегда обрабатывайте ошибки:
```javascript
asyncFunction().catch(console.error); // Fire and forget безопасно
```
</details>

<details>
<summary><b>Как отменить Promise?</b></summary>

Сами промисы отменить нельзя. Используйте AbortController для fetch:
```javascript
const controller = new AbortController();
fetch(url, { signal: controller.signal });
controller.abort(); // Отменяет fetch
```
Для кастомных промисов используйте токены отмены или проверяйте флаг перед resolve.
</details>

<details>
<summary><b>Что такое async iterators?</b></summary>

Позволяют итерировать по асинхронным источникам данных с `for await...of`:
```javascript
async function* asyncGenerator() {
  yield await fetch('/api/1').then(r => r.json());
  yield await fetch('/api/2').then(r => r.json());
}
for await (const data of asyncGenerator()) {
  console.log(data);
}
```
Полезно для потоковых данных, пагинированных API, WebSocket сообщений.
</details>

<details>
<summary><b>Что такое Promises и как они работают?</b></summary>

Promise представляет будущее завершение/неудачу асинхронной операции. Состояния: pending → fulfilled/rejected. Используйте `.then()` для успеха, `.catch()` для ошибки, `.finally()` для cleanup. Создаётся через `new Promise((resolve, reject) => {})`.
</details>

<details>
<summary><b>Что такое Promise chaining?</b></summary>

Связывание нескольких `.then()` вызовов. Каждый `.then()` возвращает новый Promise. Значение, возвращённое из одного, становится входом для следующего. Ошибки пробрасываются вниз к ближайшему `.catch()`. Чище, чем вложенные callbacks.
</details>

## Date и Math

<details>
<summary><b>Как работать с датами в JavaScript?</b></summary>

`new Date()` создаёт объект даты. Методы: `getFullYear()`, `getMonth()` (0-11), `getDate()`, `getTime()` (timestamp). Для сложных операций используйте библиотеки типа date-fns или dayjs.
</details>

<details>
<summary><b>Какие распространённые методы Math вы используете?</b></summary>

`Math.round()`, `Math.floor()`, `Math.ceil()`, `Math.random()` (0-1), `Math.max()`, `Math.min()`, `Math.abs()`, `Math.pow()`, `Math.sqrt()`.
</details>

## Object

<details>
<summary><b>Как итерировать по свойствам объекта?</b></summary>

- `Object.keys(obj)` — массив ключей
- `Object.values(obj)` — массив значений
- `Object.entries(obj)` — массив пар [key, value]
- цикл `for...in` (включает унаследованные)
</details>

<details>
<summary><b>В чём разница между Object.freeze и Object.seal?</b></summary>

- `Object.freeze()`: Нельзя добавлять, удалять или изменять свойства. Shallow freeze
- `Object.seal()`: Нельзя добавлять или удалять свойства, но МОЖНО изменять существующие
</details>

## HTTP / HTTPS

<details>
<summary><b>В чём разница между HTTP и HTTPS?</b></summary>

HTTP — базовый протокол веб-коммуникации. HTTPS добавляет шифрование (TLS/SSL) и безопасность. Современные сайты требуют HTTPS для: безопасности, SEO-рейтинга, браузерных фич (geolocation, service workers), доверия пользователей.
</details>

## Web Sockets

<details>
<summary><b>Что такое WebSockets и когда их использовать?</b></summary>

WebSocket обеспечивает full-duplex канал связи через одно TCP-соединение. Сервер может отправлять данные клиенту без запроса. Используйте для: real-time приложений, чатов, live-лент, игр, совместного редактирования. Эффективнее polling.
</details>

<details>
<summary><b>Что такое Server-Sent Events (SSE) и чем они отличаются от WebSockets?</b></summary>

SSE — технология server push для односторонней связи от сервера к клиенту через HTTP.

**Характеристики SSE:**
- Однонаправленные (только сервер → клиент)
- Построены на HTTP, проще WebSockets
- Автоматическое переподключение
- Текстовый формат (UTF-8)
- Встроенная браузерная поддержка через `EventSource` API

**Использование:**
```javascript
const eventSource = new EventSource('/events');
eventSource.onmessage = (event) => console.log(event.data);
eventSource.onerror = () => console.log('Connection error');
```

**SSE vs WebSockets:**
| Особенность | SSE | WebSocket |
|-------------|-----|-----------|
| Направление | Сервер → Клиент | Двунаправленное |
| Протокол | HTTP | WS/WSS |
| Сложность | Простой | Сложнее |
| Переподключение | Автоматическое | Ручное |
| Формат данных | Только текст | Текст + Binary |

Используйте SSE для: live-лент, уведомлений, биржевых тикеров. Используйте WebSockets для: чатов, игр, совместного редактирования.
</details>

## Functional Programming

<details>
<summary><b>Каковы принципы функционального программирования?</b></summary>

- Pure functions (без побочных эффектов)
- Иммутабельность (не мутировать данные)
- First-class functions (функции как значения)
- Higher-order functions (map, filter, reduce)
- Избегать shared state
- Декларативный подход вместо императивного
</details>

<details>
<summary><b>Что такое pure functions?</b></summary>

Pure function: один и тот же вход всегда даёт один и тот же выход, без побочных эффектов (не изменяет внешнее состояние). Легко тестировать, предсказуемы, кэшируемы. Пример: `const add = (a, b) => a + b`.
</details>

## OOP и Prototypes

<details>
<summary><b>Объясните прототипное наследование в JavaScript</b></summary>

Каждый объект имеет скрытый `[[Prototype]]`, связывающий его с другим объектом. Когда свойство не найдено, JS ищет вверх по цепочке прототипов. `Object.create(proto)` создаёт объект с указанным прототипом. Классы — синтаксический сахар над прототипами.
</details>

<details>
<summary><b>В чём разница между __proto__ и prototype?</b></summary>

**`__proto__`** — существует у каждого объекта:
- Ссылка на прототип объекта
- Используется в runtime для поиска свойств
- `obj.__proto__ === Constructor.prototype`

**`prototype`** — существует только у функций (конструкторов):
- Объект, который становится `__proto__` у экземпляров, созданных через `new`
- Используется для добавления методов, общих для всех экземпляров

```javascript
function Player(name) {
  this.name = name;
}
Player.prototype.play = function() { console.log('play'); };

const p1 = new Player('Alex');
p1.__proto__ === Player.prototype; // true
```

**Поиск по цепочке прототипов:**
1. Проверяем сам объект
2. Проверяем `__proto__`
3. Проверяем `__proto__.__proto__`
4. Продолжаем до `null`

**Важные замечания:**
- Не используйте `__proto__` напрямую — используйте `Object.getPrototypeOf()` / `Object.setPrototypeOf()`
- Изменение прототипа после создания объекта медленное
- Классы — синтаксический сахар — методы `class` попадают в `Constructor.prototype`

**Ответ для собеседования:** `prototype` — свойство функций-конструкторов, определяющее общие методы, а `__proto__` — ссылка каждого объекта на его прототип, используемая для наследования.
</details>

<details>
<summary><b>Как работают classes и super?</b></summary>

Синтаксис `class` для создания объектов. `constructor()` инициализирует экземпляр. `extends` для наследования. `super()` вызывает родительский конструктор (обязателен в дочернем конструкторе перед использованием `this`). `super.method()` вызывает метод родителя.
</details>

## Async и производительность

<details>
<summary><b>Объясните модель конкурентности и event loop</b></summary>

JS однопоточный. Event loop обрабатывает асинхронные операции. Call stack выполняет код. Web API обрабатывают async-задачи. Task queue (macrotasks) и microtask queue. Microtasks (промисы) выполняются раньше macrotasks (setTimeout). Event loop перемещает задачи в stack, когда он пуст.
</details>

<details>
<summary><b>Что такое async и await?</b></summary>

Синтаксический сахар над Promises. `async` функция всегда возвращает Promise. `await` приостанавливает выполнение до разрешения Promise. Чище, чем цепочки `.then()`. Используйте `try/catch` для обработки ошибок. `await` можно использовать только внутри `async` функции.
</details>

<details>
<summary><b>Что такое оптимизация Promise и promisification?</b></summary>

- **Promise.all()**: Запуск промисов параллельно, fail если любой fail
- **Promise.allSettled()**: Ждёт все, получает все результаты
- **Promise.race()**: Первый завершившийся побеждает
- **Promisification**: Преобразование callback-функции в возвращающую Promise
</details>

## Destructuring и Template Strings

<details>
<summary><b>Объясните деструктуризацию</b></summary>

Извлечение значений из массивов/объектов в переменные. Массивы: `const [a, b] = [1, 2]`. Объекты: `const {name, age} = user`. Можно задавать defaults: `const {name = 'unknown'} = obj`. Возможна вложенная деструктуризация.
</details>

<details>
<summary><b>Что такое template strings/literals?</b></summary>

Строки с обратными кавычками. Фичи: встраивание выражений `${variable}`, многострочные строки, tagged templates. Пример: `` `Hello ${name}, you are ${age} years old` ``.
</details>

## Modules

<details>
<summary><b>Как работают import и export в JavaScript?</b></summary>

- Named export: `export const foo = 1;` → `import { foo } from './file'`
- Default export: `export default function() {}` → `import myFunc from './file'`
- Можно переименовывать: `import { foo as bar } from './file'`
- Import всего: `import * as utils from './file'`
</details>

<details>
<summary><b>В чём разница между CommonJS и ES modules?</b></summary>

- **CommonJS**: `require()`/`module.exports`, синхронный, Node.js, динамический
- **ES modules**: `import`/`export`, async, статический (позволяет tree shaking), современный стандарт
</details>

## Proxy и Reflect

<details>
<summary><b>Что такое Proxy в JavaScript?</b></summary>

Proxy оборачивает объект и перехватывает операции. Определяет кастомное поведение для: get, set, delete, вызовов функций и т.д. Используйте для: валидации, логирования, data binding, отрицательных индексов массива.
</details>

<details>
<summary><b>Что такое Reflect и как его использовать?</b></summary>

Reflect предоставляет методы для перехватываемых операций. Те же методы, что у Proxy handlers. Чище, чем методы Object. Пример: `Reflect.get(obj, 'prop')`, `Reflect.set(obj, 'prop', value)`.
</details>

## WeakMap и WeakSet

<details>
<summary><b>В чём разница между WeakMap и Map?</b></summary>

- **WeakMap**: Только объекты в качестве ключей, ключи слабо удерживаются (garbage collected если нет других ссылок), не итерируемый, нет `size`
- Используйте для: приватных данных, кэширования без утечек памяти
</details>

<details>
<summary><b>Когда использовать WeakSet?</b></summary>

Хранение объектов без предотвращения garbage collection. Используйте для: отслеживания посещённых объектов, пометки объектов как обработанных. Элементы автоматически удаляются, когда у объекта нет других ссылок.
</details>

## Regular Expressions

<details>
<summary><b>Как использовать регулярные выражения в JavaScript?</b></summary>

Создание: `/pattern/flags` или `new RegExp()`. Методы: `test()` возвращает boolean, `match()` возвращает совпадения, `replace()` заменяет. Флаги: `g` (global), `i` (case-insensitive), `m` (multiline).
</details>

## Web Workers и Service Workers

<details>
<summary><b>Что такое Web Workers?</b></summary>

Выполнение скриптов в фоновом потоке. Не блокируют UI. Не имеют доступа к DOM. Взаимодействуют через `postMessage()`. Используйте для: тяжёлых вычислений, обработки данных.
</details>

<details>
<summary><b>Что такое Service Workers и чем они отличаются?</b></summary>

Специальные workers, действующие как proxy между приложением и сетью. Обеспечивают: offline-поддержку, кэширование, push-уведомления, background sync. Lifecycle: install → activate → fetch. **Требуют HTTPS** (кроме localhost). Обязательны для PWA.
</details>

## Dependency Injection

<details>
<summary><b>Объясните различные модульные системы (CommonJS, AMD, namespace)</b></summary>

- **CommonJS**: `require/exports`, синхронный, Node.js
- **AMD**: `define/require`, асинхронный, браузер (RequireJS)
- **Namespace**: Паттерн глобального объекта, старый подход. `MyApp.utils.foo()`
</details>

## Storage

<details>
<summary><b>В чём разница между LocalStorage и SessionStorage?</b></summary>

- **LocalStorage**: Сохраняется пока не очищен вручную, ~5MB, same-origin
- **SessionStorage**: Очищается при закрытии вкладки, изоляция по вкладкам
- Оба: синхронные, только строки (используйте JSON.stringify)
</details>

<details>
<summary><b>В чём разница между Cookies, sessionStorage и localStorage?</b></summary>

- **Cookies**: Отправляются с каждым HTTP-запросом, поддерживают опции безопасности (HttpOnly, Secure, SameSite), макс ~4KB, можно задать срок действия
- **sessionStorage**: Живёт до закрытия вкладки, ~5MB, не отправляется на сервер
- **localStorage**: Сохраняет данные постоянно в браузере, ~5MB, не отправляется на сервер

Используйте cookies для auth-токенов (с HttpOnly), storage API для клиентских данных.
</details>

## Memory Management

<details>
<summary><b>Как работает garbage collection в JavaScript?</b></summary>

Автоматическое управление памятью. Алгоритм mark-and-sweep: помечает достижимые объекты, очищает непомеченные. Запускается периодически. Объекты без ссылок собираются.
</details>

<details>
<summary><b>Как предотвратить утечки памяти?</b></summary>

Распространённые причины и решения:
- Удаляйте event listeners когда закончили
- Очищайте intervals/timeouts
- Избегайте глобальных переменных
- Очищайте closures
- Обнуляйте ссылки на большие объекты
- Используйте WeakMap/WeakSet для кэшей
</details>

## Generators и Iterators

<details>
<summary><b>Что такое generators и как их использовать?</b></summary>

Функции, которые могут приостанавливаться и возобновляться. Используйте `function*` и `yield`. Возвращает iterator. `next()` продолжает выполнение. Используйте для: lazy evaluation, бесконечных последовательностей, async flows.
</details>

<details>
<summary><b>Что такое iterators?</b></summary>

Объект с методом `next()`, возвращающим `{value, done}`. Делает объект итерируемым через `for...of`. Реализуйте `[Symbol.iterator]` для создания кастомных итерируемых объектов.
</details>

## Приведение типов

<details>
<summary><b>Что делает !!variable?</b></summary>

Двойное отрицание преобразует значение в boolean. Первый `!` конвертит в boolean и инвертирует, второй `!` инвертирует обратно. То же что `Boolean(value)`:
```javascript
!!0        // false
!!"hello"  // true
!!null     // false
!!{}       // true
```
</details>

<details>
<summary><b>Что выдаст [] + {} vs {} + []?</b></summary>

```javascript
[] + {}  // "[object Object]" - массив в "", объект в строку
{} + []  // 0 - {} это пустой блок, +[] это 0
```
Хитрость в том, что `{}` в начале парсится как блок кода, не объект. Оберните в скобки: `({}) + []` даст "[object Object]".
</details>

<details>
<summary><b>Как безопасно проверить null и undefined?</b></summary>

```javascript
// Проверка обоих (нестрогое равенство)
if (value == null) { } // ловит null и undefined

// Nullish coalescing (ES2020)
const result = value ?? 'default'; // только null/undefined

// Optional chaining
const name = user?.profile?.name;
```
</details>

<details>
<summary><b>Чем Number() отличается от parseInt()?</b></summary>

- `Number()`: Конвертирует всю строку, возвращает NaN при любом нечисловом символе
- `parseInt()`: Парсит с начала, останавливается на нечисловом символе

```javascript
Number("42px")   // NaN
parseInt("42px") // 42
Number("")       // 0
parseInt("")     // NaN
```
</details>

## Продвинутые методы массивов

<details>
<summary><b>Какая Big O сложность цепочки методов массива?</b></summary>

Каждый метод итерирует весь массив: O(n) на метод. Цепочка `map().filter().reduce()` = O(3n) = O(n), но с 3x итерациями. Для больших массивов используйте один `reduce()` или for-цикл для обработки за один проход.
</details>

<details>
<summary><b>Что будет если не вернуть ничего из callback map?</b></summary>

Вернёт `undefined` для этого элемента. Длина массива та же, но значения undefined:
```javascript
[1, 2, 3].map(x => { x * 2 }); // [undefined, undefined, undefined]
[1, 2, 3].map(x => x * 2);      // [2, 4, 6]
```
Частая ошибка: забыть return в многострочных arrow functions.
</details>

<details>
<summary><b>Что такое flatMap и flat методы?</b></summary>

- `flat(depth)`: Выравнивает вложенные массивы на указанную глубину (по умолчанию 1)
- `flatMap(fn)`: map + flat на один уровень. Эффективнее чем `.map().flat()`

```javascript
[[1], [2, 3]].flat();           // [1, 2, 3]
[1, 2].flatMap(x => [x, x*2]);  // [1, 2, 2, 4]
```
</details>

<details>
<summary><b>Как отсортировать объекты по свойству?</b></summary>

Передайте функцию сравнения в sort:
```javascript
const users = [{name: 'Bob', age: 30}, {name: 'Alice', age: 25}];
users.sort((a, b) => a.age - b.age); // По возрасту
users.sort((a, b) => a.name.localeCompare(b.name)); // По имени
```
Важно: `sort()` мутирует оригинальный массив.
</details>

## Symbols

<details>
<summary><b>Что такое Symbols и когда их использовать?</b></summary>

Уникальный, иммутабельный примитив. `Symbol('description')`. Используйте для: приватных свойств, избежания коллизий имён, well-known symbols (`Symbol.iterator`, `Symbol.toStringTag`).
</details>

<details>
<summary><b>Что такое Symbol?</b></summary>

Symbol — уникальное значение, используемое как ключ свойства в объектах. Помогает предотвратить конфликты имён, особенно в shared-коде типа библиотек. Каждый Symbol всегда уникален, даже с одинаковым именем. `Symbol('a') !== Symbol('a')`.
</details>

## Iterators

<details>
<summary><b>Что такое Iterators?</b></summary>

Iterator — объект, позволяющий читать значения по одному. Следует простому правилу с методом `next()`, возвращающим `{value, done}`. Iterators используются в `for...of` циклах и других встроенных фичах типа spread-оператора.
</details>

## NaN

<details>
<summary><b>Что такое NaN?</b></summary>

NaN означает "Not a Number". Появляется при неудачных вычислениях (например, `0/0`, `parseInt('abc')`). NaN особенный, потому что не равен самому себе (`NaN !== NaN`). Используйте `Number.isNaN()` для проверки на NaN.
</details>

## IIFE

<details>
<summary><b>Что такое IIFE?</b></summary>

IIFE (Immediately Invoked Function Expression) — функция, которая выполняется сразу после определения. Использовалась для создания приватных переменных до появления современного синтаксиса. Пример: `(function() { var private = 1; })()`. Сейчас встречается в основном в старом коде.
</details>

## Event Loop

<details>
<summary><b>Что такое Event Loop?</b></summary>

Event loop контролирует порядок выполнения JavaScript-кода. Сначала обрабатывает синхронный код, затем microtasks (промисы), затем macrotasks (setTimeout, setInterval). Это позволяет JavaScript быть неблокирующим, несмотря на однопоточность.
</details>

## DOM

<details>
<summary><b>Что такое DOM?</b></summary>

DOM (Document Object Model) представляет веб-страницу как древовидную структуру. JavaScript использует его для чтения и обновления UI. DOM-операции могут быть медленными при чрезмерном использовании — поэтому фреймворки типа React используют Virtual DOM.
</details>

## Event Bubbling

<details>
<summary><b>Что такое Event Bubbling?</b></summary>

События движутся от целевого элемента вверх к родительским элементам. Это позволяет использовать event delegation — прикрепить один listener к родителю вместо многих к детям. Bubbling можно остановить через `event.stopPropagation()` при необходимости.
</details>

## JSONP

<details>
<summary><b>Что такое JSONP?</b></summary>

JSONP — старая техника загрузки данных между доменами до появления CORS. Использует script-теги и callbacks. Небезопасна (выполняет произвольный код) и редко используется сегодня. CORS — современное решение.
</details>

## Immutability

<details>
<summary><b>Что такое Immutability?</b></summary>

Immutability означает не изменять существующие данные. Вместо этого создаются новые данные. Это упрощает отслеживание и отладку изменений состояния. Пример: вместо `arr.push(item)` используйте `[...arr, item]`. Важно для управления state в React.
</details>

## File APIs

<details>
<summary><b>Что такое FileSystem API?</b></summary>

Browser API для чтения/записи файлов в sandboxed файловую систему. Ограниченная браузерная поддержка. Современный File System Access API позволяет доступ к файлам пользователя с разрешения.
</details>

<details>
<summary><b>Что такое FileReader API?</b></summary>

Асинхронное чтение содержимого файлов. Методы: `readAsText()`, `readAsDataURL()`, `readAsArrayBuffer()`. События: `onload`, `onerror`. Используйте с file input или drag-drop.
</details>

## GraphQL

<details>
<summary><b>Что такое GraphQL?</b></summary>

GraphQL позволяет клиентам запрашивать именно те данные, которые им нужны. Использует единый endpoint вместо множества REST endpoints. Преимущества: нет over-fetching/under-fetching, строго типизированная схема, интроспекция. Trade-off: добавляет сложность на сервере, кэширование сложнее, чем в REST.
</details>

## Design Patterns

<details>
<summary><b>Какие design patterns вы используете в JavaScript?</b></summary>

Распространённые паттерны:
- **Module**: Инкапсуляция кода, private/public
- **Singleton**: Единственный экземпляр
- **Observer**: Publish/subscribe события
- **Factory**: Создание объектов без указания класса
- **Decorator**: Добавление поведения объектам
</details>

## Продвинутый Event Loop

<details>
<summary><b>Объясните поведение event loop с вложенными промисами + setTimeout + async/await</b></summary>

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
// Вывод: 1, 5, 7, 3, 6, 4, 2
```

**Порядок выполнения:**
1. Синхронный код выполняется первым (1, 5, 7)
2. `await` приостанавливает `foo()`, планирует продолжение как microtask
3. Microtasks выполняются раньше macrotasks: callbacks промисов (3), затем продолжение `foo` (6), затем вложенный промис (4)
4. Macrotasks (setTimeout) выполняются последними (2)

**Ключевое правило:** Очередь microtasks (промисы) полностью опустошается перед каждым macrotask (setTimeout, setInterval).
</details>

## Реализации утилит

<details>
<summary><b>Реализуйте функции debounce, throttle и memoize</b></summary>

**Debounce** — задерживает выполнение до паузы в вызовах:
```javascript
function debounce(fn, delay) {
  let timeoutId;
  return function(...args) {
    clearTimeout(timeoutId);
    timeoutId = setTimeout(() => fn.apply(this, args), delay);
  };
}
```

**Throttle** — ограничивает выполнение до одного раза за период:
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

**Memoize** — кэширует результаты функции:
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
<summary><b>Реализуйте кастомную функцию curry</b></summary>

Каррирование преобразует `f(a, b, c)` в `f(a)(b)(c)`:

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

// Использование
const sum = (a, b, c) => a + b + c;
const curriedSum = curry(sum);
curriedSum(1)(2)(3); // 6
curriedSum(1, 2)(3); // 6
curriedSum(1)(2, 3); // 6
```
</details>

<details>
<summary><b>Напишите функцию глубокого клонирования без использования lodash</b></summary>

```javascript
function deepClone(obj, seen = new WeakMap()) {
  // Обработка примитивов и null
  if (obj === null || typeof obj !== 'object') return obj;

  // Обработка циклических ссылок
  if (seen.has(obj)) return seen.get(obj);

  // Обработка Date
  if (obj instanceof Date) return new Date(obj);

  // Обработка RegExp
  if (obj instanceof RegExp) return new RegExp(obj);

  // Обработка Array и Object
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

**Обрабатываемые edge cases:** циклические ссылки, Date, RegExp, вложенные объекты/массивы. Примечание: не обрабатывает Map, Set, функции или цепочку прототипов.
</details>

<details>
<summary><b>Что происходит внутри при вызове `new`?</b></summary>

При вызове `new Constructor()`:

1. **Создание пустого объекта**: `const obj = {}`
2. **Связывание прототипа**: `obj.__proto__ = Constructor.prototype`
3. **Привязка `this`**: Выполнение конструктора с `this`, привязанным к `obj`
4. **Возврат объекта**: Возврат `obj` (если конструктор не вернул другой объект)

```javascript
function myNew(Constructor, ...args) {
  // 1. Создание нового объекта
  const obj = {};
  // 2. Связывание прототипа
  Object.setPrototypeOf(obj, Constructor.prototype);
  // 3. Выполнение конструктора с this = obj
  const result = Constructor.apply(obj, args);
  // 4. Возврат объекта (или возврата конструктора, если это объект)
  return result instanceof Object ? result : obj;
}
```
</details>

<details>
<summary><b>Реализуйте свои Promise.all, Promise.race, Promise.any</b></summary>

```javascript
// Promise.all - резолвится когда все резолвятся, реджектится при первом реджекте
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

// Promise.race - резолвится/реджектится с первым завершённым
Promise.myRace = function(promises) {
  return new Promise((resolve, reject) => {
    promises.forEach(promise => {
      Promise.resolve(promise).then(resolve).catch(reject);
    });
  });
};

// Promise.any - резолвится с первым fulfilled, реджектится если все реджектнулись
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
<summary><b>Как бы вы спроектировали систему плагинов используя closures?</b></summary>

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

// Использование
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

## Продвинутые async-паттерны

<details>
<summary><b>Реализуйте API retry с экспоненциальным backoff</b></summary>

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

      // Не ретраим клиентские ошибки (4xx)
      if (error.message?.includes('4')) throw error;

      // Экспоненциальный backoff: 1s, 2s, 4s...
      const delay = Math.pow(2, attempt) * 1000;
      const jitter = Math.random() * 1000; // Добавляем случайность

      console.log(`Retry ${attempt + 1}/${maxRetries} через ${delay}ms`);
      await new Promise(r => setTimeout(r, delay + jitter));
    }
  }

  throw lastError;
}
```
</details>

<details>
<summary><b>Как отменить текущие API-запросы при смене роута?</b></summary>

Используйте **AbortController** для отмены fetch-запросов:

```javascript
// Создаём controller для роута/компонента
const controller = new AbortController();

// Передаём signal в fetch
fetch('/api/data', { signal: controller.signal })
  .then(res => res.json())
  .catch(err => {
    if (err.name === 'AbortError') {
      console.log('Запрос отменён');
    }
  });

// Отмена при смене роута/cleanup
controller.abort();

// Пример в React
useEffect(() => {
  const controller = new AbortController();

  fetch('/api/data', { signal: controller.signal })
    .then(res => res.json())
    .then(setData);

  return () => controller.abort(); // Cleanup
}, []);
```

Для нескольких запросов создавайте новый controller для каждой группы или используйте менеджер запросов.
</details>

<details>
<summary><b>Спроектируйте слой кэширования для часто используемых API</b></summary>

```javascript
class APICache {
  constructor(ttl = 60000) { // По умолчанию TTL 1 минута
    this.cache = new Map();
    this.ttl = ttl;
  }

  async fetch(url, options = {}) {
    const key = this.createKey(url, options);
    const cached = this.cache.get(key);

    // Возвращаем из кэша если валидно
    if (cached && Date.now() < cached.expiry) {
      return cached.data;
    }

    // Получаем свежие данные
    const response = await fetch(url, options);
    const data = await response.json();

    // Кэшируем результат
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

Рассмотрите: LRU-вытеснение, stale-while-revalidate, теги кэша для групповой инвалидации.
</details>

<details>
<summary><b>Как объединить несколько API-запросов в один?</b></summary>

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

// Использование — batch запросов пользователей
const userBatcher = new RequestBatcher(
  async (ids) => fetch(`/api/users?ids=${ids.join(',')}`).then(r => r.json())
);

// Эти вызовы будут объединены в один запрос
userBatcher.add(1).then(user => console.log(user));
userBatcher.add(2).then(user => console.log(user));
```
</details>

## Задачи с кодом

<details>
<summary><b>Создайте мини SPA роутер на JavaScript</b></summary>

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
    // Преобразуем /users/:id в regex
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

// Использование
const router = new Router();
router.addRoute('/', () => console.log('Главная'));
router.addRoute('/users/:id', ({ id }) => console.log(`Пользователь ${id}`));
router.addRoute('*', () => console.log('404'));
router.navigate(location.pathname);
```
</details>

<details>
<summary><b>Реализуйте мини Redux store с subscribe, dispatch, reducer</b></summary>

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
      // Возвращаем функцию отписки
      return () => {
        listeners = listeners.filter(l => l !== listener);
      };
    }
  };
}

// Использование
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
<summary><b>Напишите алгоритм diff для сравнения двух JSON-объектов</b></summary>

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

// Использование
const old = { a: 1, b: { c: 2 }, d: 3 };
const current = { a: 1, b: { c: 5 }, e: 4 };
console.log(diff(old, current));
// [{ type: 'CHANGED', path: 'b.c', oldValue: 2, newValue: 5 },
//  { type: 'DELETED', path: 'd', oldValue: 3 },
//  { type: 'ADDED', path: 'e', newValue: 4 }]
```
</details>

<details>
<summary><b>Реализуйте async memoization, обрабатывающую параллельные запросы</b></summary>

Async memoization кэширует результаты async-функций и корректно обрабатывает параллельные вызовы:

```javascript
function memoizeAsync(fn) {
  const cache = new Map();
  const pending = new Map();

  return function(...args) {
    const key = JSON.stringify(args);

    // Возвращаем кэшированный результат
    if (cache.has(key)) {
      return Promise.resolve(cache.get(key));
    }

    // Возвращаем pending promise если запрос в процессе
    if (pending.has(key)) {
      return pending.get(key);
    }

    // Выполняем новый запрос
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

// Использование
const memoizedFetch = memoizeAsync(async (userId) => {
  const res = await fetch(`/api/users/${userId}`);
  return res.json();
});

// Эти вызовы используют один запрос (дедупликация)
memoizedFetch(1); // Делает запрос
memoizedFetch(1); // Возвращает тот же pending promise
memoizedFetch(1); // Возвращает тот же pending promise
```

**Ключевые особенности:**
- Кэширует успешные результаты
- Дедуплицирует параллельные запросы с одинаковыми аргументами
- Удаляет pending-состояние при ошибке (позволяет retry)
- Использует JSON.stringify для глубокого сравнения ключей
</details>

<details>
<summary><b>Реализуйте поиск по мере ввода с кэшированием + debounce</b></summary>

```javascript
function createSearchHandler(searchFn, debounceMs = 300) {
  const cache = new Map();
  let timeoutId;
  let abortController;

  return async function search(query, onResults) {
    // Очищаем предыдущий timeout
    clearTimeout(timeoutId);

    // Отменяем предыдущий запрос
    abortController?.abort();

    if (!query.trim()) {
      onResults([]);
      return;
    }

    // Проверяем кэш
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

// Использование
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
