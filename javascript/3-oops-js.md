Great set of questions! Here's a comprehensive explanation of key **Object-Oriented and Functional JavaScript** concepts:

---

### **1. How does prototypal inheritance work in JavaScript?**

**Prototypal inheritance** is a feature where objects inherit properties and methods from other objects.

In JavaScript, every object has an internal link to another object called its **prototype**.

#### ✅ Example:

```javascript
const animal = {
  eats: true,
};

const dog = Object.create(animal);
dog.barks = true;

console.log(dog.eats); // true (inherited)
```

#### 🔍 Explanation:

* `dog` doesn't have `eats`, so it looks up the **prototype chain** and finds it in `animal`.
* This is how **inheritance** is achieved in JS (not via classes like in traditional OOP).

---

### **2. What is the difference between a class and a constructor function?**

#### ✅ Constructor Function:

```javascript
function Person(name) {
  this.name = name;
}
Person.prototype.sayHi = function () {
  console.log(`Hi, I'm ${this.name}`);
};
```

#### ✅ ES6 Class:

```javascript
class Person {
  constructor(name) {
    this.name = name;
  }
  sayHi() {
    console.log(`Hi, I'm ${this.name}`);
  }
}
```

#### 🔍 Key Differences:

| Feature           | Constructor Function                           | ES6 Class Syntax                 |
| ----------------- | ---------------------------------------------- | -------------------------------- |
| Syntax            | Function-based                                 | More declarative, cleaner syntax |
| Inheritance       | Manually with `Object.create()` or `prototype` | `extends` and `super()` keywords |
| Behind the scenes | Just syntactic sugar over prototypes           | Still uses prototype internally  |
| Hoisting          | Hoisted                                        | Not hoisted                      |

---

### **3. What is the purpose of `Object.create()`?**

`Object.create(proto)` creates a **new object** with the specified prototype.

#### ✅ Example:

```javascript
const animal = {
  eats: true,
};

const rabbit = Object.create(animal);
rabbit.hops = true;

console.log(rabbit.eats); // true (from prototype)
```

#### 🔍 Purpose:

* Allows setting an object’s prototype directly.
* Useful for **creating inheritance** without using classes or constructor functions.

---

### **4. Explain `call`, `apply`, and `bind` methods.**

These methods allow **explicit setting of `this`** context.

#### ✅ `call()`: invokes function with `this` and arguments separately

```javascript
function greet(greeting) {
  console.log(`${greeting}, ${this.name}`);
}
const person = { name: 'Alice' };
greet.call(person, 'Hello'); // Hello, Alice
```

#### ✅ `apply()`: same as `call` but arguments passed as array

```javascript
greet.apply(person, ['Hi']); // Hi, Alice
```

#### ✅ `bind()`: returns a new function with bound `this`

```javascript
const greetAlice = greet.bind(person);
greetAlice('Hey'); // Hey, Alice
```

---

### **5. What are pure functions?**

A **pure function**:

* **Always returns the same output** for the same input.
* Has **no side effects** (e.g., modifying external state, DOM, or global variables).

#### ✅ Example:

```javascript
function add(a, b) {
  return a + b;
}
```

#### ❌ Impure function example:

```javascript
let counter = 0;
function increment() {
  return ++counter;
}
```

#### 🔍 Benefits:

* Easier to test, debug, and reason about.
* Promotes **functional programming** style.

---

### **6. What is immutability and how can it be enforced in JavaScript?**

**Immutability** means data **cannot be changed** once created.

#### ✅ Enforcing immutability:

**a. Using `const` (for binding, not deep immutability)**:

```javascript
const arr = [1, 2];
// arr = [3, 4]; ❌ Error
arr.push(3); // ✅ Still allowed, not deeply immutable
```

**b. Object.freeze()**:

```javascript
const obj = Object.freeze({ name: 'John' });
obj.name = 'Doe'; // ❌ No effect
```

**c. Immutable updates using spread or utility libs**:

```javascript
const user = { name: 'Alice' };
const updatedUser = { ...user, age: 30 };
```

**d. Libraries**:

* [Immer](https://immerjs.github.io/immer/)
* [Immutable.js](https://immutable-js.github.io/immutable-js/)

---

