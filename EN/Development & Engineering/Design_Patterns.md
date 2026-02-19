# Design Patterns Interview Questions

## Design Patterns Overview

<details>
<summary><b>What are design patterns and why are they useful?</b></summary>

Design patterns are reusable solutions to common problems. Not code, but templates/concepts. Benefits: proven solutions, shared vocabulary, avoid reinventing wheel, easier communication, maintainable code. Don't overuse - adds complexity if not needed.
</details>

<details>
<summary><b>List and explain different design patterns (Creational, Structural, Behavioral)</b></summary>

- **Creational**: Object creation. Factory, Singleton, Builder, Prototype
- **Structural**: Object composition. Adapter, Decorator, Facade, Proxy
- **Behavioral**: Object communication. Observer, Strategy, Command, Iterator
</details>

<details>
<summary><b>How do you choose the right design pattern for a specific task?</b></summary>

Identify the problem type first. Creational: complex object creation. Structural: incompatible interfaces, adding features. Behavioral: communication between objects. Consider: simplicity, team familiarity, future flexibility. Don't force patterns.
</details>

## Module Pattern

<details>
<summary><b>Explain the Module pattern</b></summary>

Encapsulates code with private and public members. Uses closure to create private scope. Example:
```javascript
const module = (function() {
  let privateVar = 0;
  return {
    publicMethod() { return privateVar; }
  };
})();
```
Modern alternative: ES modules with import/export.
</details>

## Prototype Pattern

<details>
<summary><b>Explain the Prototype pattern</b></summary>

Create objects by cloning existing object (prototype). Useful when: object creation is expensive, need similar objects with small differences. JavaScript uses prototype inheritance natively. `Object.create(proto)` creates object with specified prototype.
</details>

## Singleton Pattern

<details>
<summary><b>Explain the Singleton pattern</b></summary>

Ensure class has only one instance. Provide global access point. Example: database connection, configuration object, logger.
```javascript
class Singleton {
  static instance;
  static getInstance() {
    if (!this.instance) this.instance = new Singleton();
    return this.instance;
  }
}
```
In modules, simple export works as singleton.
</details>

## Practical Application

<details>
<summary><b>Give examples of when you used specific design patterns in your projects</b></summary>

Common uses:
- **Observer**: Event systems, state management
- **Factory**: Creating components based on type
- **Decorator**: HOCs in React, middleware
- **Strategy**: Different validation rules, sorting algorithms
- **Facade**: Simplified API wrapper
</details>

<details>
<summary><b>Describe your practical experience using design patterns</b></summary>

(Personal experience question - describe: patterns you've implemented, problems solved, how you decided to use them, any patterns you avoid and why.)
</details>

<details>
<summary><b>How do you decide which design pattern to use for a specific problem?</b></summary>

Steps: understand the problem, identify what varies vs. stays same, check if standard pattern fits, consider simpler solutions first. Ask: will this make code clearer or more complex? Is team familiar with it? Don't use pattern just because you can.
</details>

<details>
<summary><b>Can you refactor existing code to use appropriate design patterns?</b></summary>

Yes, when: code has clear smell (tight coupling, repetition), pattern genuinely helps, team understands benefit. Process: identify problem, choose pattern, refactor incrementally, test each step. Avoid big rewrites - small improvements over time.
</details>
