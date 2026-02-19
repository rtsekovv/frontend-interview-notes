# Вопросы для собеседования по Design Patterns

## Обзор Design Patterns

<details>
<summary><b>Что такое design patterns и почему они полезны?</b></summary>

Design patterns — это переиспользуемые решения распространённых проблем. Не код, а шаблоны/концепции. Преимущества: проверенные решения, общий словарь, не нужно изобретать велосипед, проще коммуникация, поддерживаемый код. Не злоупотребляйте — добавляет сложность если не нужно.
</details>

<details>
<summary><b>Перечислите и объясните разные design patterns (Creational, Structural, Behavioral)</b></summary>

- **Creational**: Создание объектов. Factory, Singleton, Builder, Prototype
- **Structural**: Композиция объектов. Adapter, Decorator, Facade, Proxy
- **Behavioral**: Коммуникация объектов. Observer, Strategy, Command, Iterator
</details>

<details>
<summary><b>Как выбрать правильный design pattern для конкретной задачи?</b></summary>

Сначала определите тип проблемы. Creational: сложное создание объектов. Structural: несовместимые интерфейсы, добавление фич. Behavioral: коммуникация между объектами. Учитывайте: простоту, знакомство команды, будущую гибкость. Не навязывайте паттерны.
</details>

## Module Pattern

<details>
<summary><b>Объясните Module pattern</b></summary>

Инкапсулирует код с private и public членами. Использует closure для создания private scope. Пример:
```javascript
const module = (function() {
  let privateVar = 0;
  return {
    publicMethod() { return privateVar; }
  };
})();
```
Современная альтернатива: ES modules с import/export.
</details>

## Prototype Pattern

<details>
<summary><b>Объясните Prototype pattern</b></summary>

Создание объектов клонированием существующего объекта (прототипа). Полезен когда: создание объекта дорогое, нужны похожие объекты с небольшими отличиями. JavaScript использует прототипное наследование нативно. `Object.create(proto)` создаёт объект с указанным прототипом.
</details>

## Singleton Pattern

<details>
<summary><b>Объясните Singleton pattern</b></summary>

Гарантирует что класс имеет только один экземпляр. Предоставляет глобальную точку доступа. Примеры: database connection, объект конфигурации, logger.
```javascript
class Singleton {
  static instance;
  static getInstance() {
    if (!this.instance) this.instance = new Singleton();
    return this.instance;
  }
}
```
В модулях простой export работает как singleton.
</details>

## Практическое применение

<details>
<summary><b>Приведите примеры когда вы использовали конкретные design patterns в проектах</b></summary>

Распространённое использование:
- **Observer**: Event systems, state management
- **Factory**: Создание компонентов по типу
- **Decorator**: HOCs в React, middleware
- **Strategy**: Разные правила валидации, алгоритмы сортировки
- **Facade**: Упрощённая API-обёртка
</details>

<details>
<summary><b>Опишите ваш практический опыт использования design patterns</b></summary>

(Личный вопрос — опишите: какие паттерны реализовывали, какие проблемы решали, как принимали решение об использовании, какие паттерны избегаете и почему.)
</details>

<details>
<summary><b>Как вы решаете какой design pattern использовать для конкретной проблемы?</b></summary>

Шаги: понять проблему, определить что меняется vs остаётся неизменным, проверить подходит ли стандартный паттерн, рассмотреть более простые решения сначала. Спросите: сделает ли это код понятнее или сложнее? Знакома ли команда с этим? Не используйте паттерн только потому что можете.
</details>

<details>
<summary><b>Можете ли вы рефакторить существующий код с использованием подходящих design patterns?</b></summary>

Да, когда: код имеет явный smell (tight coupling, повторения), паттерн действительно помогает, команда понимает пользу. Процесс: определить проблему, выбрать паттерн, рефакторить инкрементально, тестировать каждый шаг. Избегайте больших переписываний — маленькие улучшения со временем.
</details>
