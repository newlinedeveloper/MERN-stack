Absolutely! Below are clear and concise **answers with explanations** to each conceptual JavaScript question:

---

### **1. What are the differences between `var`, `let`, and `const`?**

| Feature       | `var`                            | `let`                     | `const`                   |
| ------------- | -------------------------------- | ------------------------- | ------------------------- |
| Scope         | Function-scoped                  | Block-scoped              | Block-scoped              |
| Hoisting      | Yes (initialized as `undefined`) | Yes (but not initialized) | Yes (but not initialized) |
| Redeclaration | Allowed                          | Not allowed in same scope | Not allowed in same scope |
| Reassignment  | Allowed                          | Allowed                   | **Not allowed**           |

**Explanation**:

* `var` is **function-scoped** and can be re-declared.
* `let` and `const` are **block-scoped** (limited to `{}`).
* `const` must be initialized at declaration and cannot be reassigned, but objects declared with `const` **can be mutated**.

---

### **2. Explain the concept of hoisting.**

**Answer**:
Hoisting is JavaScript's default behavior of **moving declarations to the top** of the current scope before code execution.

**Example**:

```javascript
console.log(a); // undefined
var a = 10;
```

The above code is interpreted as:

```javascript
var a;
console.log(a); // undefined
a = 10;
```

**Explanation**:

* `var` is hoisted with **initialization as `undefined`**.
* `let` and `const` are hoisted but **not initialized**, so accessing them before declaration causes a **ReferenceError** (they are in the *temporal dead zone*).

---

### **3. What are closures and how are they used?**

**Answer**:
A **closure** is a function that **remembers the variables from its outer lexical scope**, even after the outer function has finished executing.

**Example**:

```javascript
function outer() {
  let count = 0;
  return function inner() {
    count++;
    return count;
  };
}
const counter = outer();
console.log(counter()); // 1
console.log(counter()); // 2
```

**Explanation**:
The `inner()` function **closes over** the `count` variable from `outer()`—this is a closure. It allows for data **encapsulation and persistence**.

---

### **4. What is the difference between `==` and `===`?**

**Answer**:

* `==` is **loose equality** – compares **value only**, with **type coercion**.
* `===` is **strict equality** – compares **value and type**.

**Example**:

```javascript
'5' == 5      // true  (type coercion)
'5' === 5     // false (no coercion)
```

**Explanation**:
Always prefer `===` to avoid unexpected behavior from type coercion.

---

### **5. What is a promise? How is it different from callbacks?**

**Answer**:
A **Promise** is an object representing the **eventual completion or failure** of an asynchronous operation.

**Syntax**:

```javascript
let promise = new Promise((resolve, reject) => {
  // async code
});
```

**Differences from callbacks**:

| Callbacks                   | Promises                     |
| --------------------------- | ---------------------------- |
| Can lead to callback hell   | Easy to chain with `.then()` |
| No error handling mechanism | Has `.catch()` for errors    |
| Harder to read and maintain | Cleaner and more readable    |

**Example**:

```javascript
fetch(url)
  .then(response => response.json())
  .catch(err => console.error(err));
```

---

### **6. What is the event loop and how does JavaScript handle asynchronous code?**

**Answer**:
The **event loop** is a mechanism that **manages execution of multiple chunks of code** (tasks), including asynchronous operations like callbacks, promises, or timers.

**Execution flow**:

1. JS runs in a **single thread**.
2. Long-running async tasks (like `setTimeout`, `fetch`) are moved to the **Web APIs**.
3. Once complete, their callback is pushed to the **callback/task queue**.
4. The **event loop** picks from the task queue when the **call stack is empty**.

**Example**:

```javascript
console.log('Start');
setTimeout(() => console.log('Timeout'), 0);
Promise.resolve().then(() => console.log('Promise'));
console.log('End');
```

**Output**:

```
Start
End
Promise
Timeout
```

**Explanation**:

* Promises (microtasks) are prioritized over `setTimeout` (macrotasks).

---

### **7. Explain the concept of lexical scoping.**

**Answer**:
Lexical scoping means that a variable’s **scope is determined by its location in the source code** and **nested functions have access** to variables defined in their outer scope.

**Example**:

```javascript
function outer() {
  let outerVar = 'outer';
  function inner() {
    console.log(outerVar); // has access
  }
  inner();
}
outer();
```

**Explanation**:
Here, `inner()` can access `outerVar` because it's **lexically scoped within** `outer()`.

---

### **8. What is currying in JavaScript?**

**Answer**:
**Currying** is a technique of transforming a function with multiple arguments into a **series of functions each taking one argument**.

**Example**:

```javascript
function add(a) {
  return function(b) {
    return a + b;
  };
}
add(2)(3); // 5
```

Or using arrow functions:

```javascript
const add = a => b => a + b;
```

**Explanation**:
Currying is useful in **function composition** and creating **reusable utility functions**.

---

Would you like these answers formatted as a PDF or need follow-up questions for practice?
