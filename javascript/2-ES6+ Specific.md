Certainly! Here's a detailed explanation and examples for each of the **ES6+ specific JavaScript concepts** you asked about:

---

### **1. What are arrow functions and how do they differ from regular functions?**

**Arrow functions** are a shorthand way to write functions in JavaScript introduced in ES6. They use the `=>` syntax.

#### ✅ Example:

```javascript
// Regular function
function add(a, b) {
  return a + b;
}

// Arrow function
const add = (a, b) => a + b;
```

#### 🔍 Differences:

| Feature                     | Regular Function                     | Arrow Function                       |
| --------------------------- | ------------------------------------ | ------------------------------------ |
| Syntax                      | Verbose                              | Concise                              |
| `this` binding              | Dynamic (depends on how it's called) | Lexical (inherits from parent scope) |
| Can be used as constructors | Yes                                  | ❌ No                                 |
| Has `arguments` object      | Yes                                  | ❌ No                                 |

#### 🔥 Most important:

Arrow functions **do not have their own `this`** — they capture the `this` value from the surrounding lexical context.

---

### **2. How do `map`, `filter`, and `reduce` work? Can you give examples?**

These are **array methods** used for **transformation and processing**.

#### ✅ `map`: transforms each element

```javascript
const nums = [1, 2, 3];
const doubled = nums.map(n => n * 2); // [2, 4, 6]
```

#### ✅ `filter`: selects elements that meet a condition

```javascript
const nums = [1, 2, 3, 4];
const even = nums.filter(n => n % 2 === 0); // [2, 4]
```

#### ✅ `reduce`: reduces array to a single value

```javascript
const nums = [1, 2, 3, 4];
const sum = nums.reduce((acc, n) => acc + n, 0); // 10
```

---

### **3. Explain destructuring assignment.**

**Destructuring** allows you to unpack values from arrays or properties from objects into distinct variables.

#### ✅ Array destructuring

```javascript
const [a, b] = [10, 20];
console.log(a); // 10
console.log(b); // 20
```

#### ✅ Object destructuring

```javascript
const user = { name: 'Alice', age: 25 };
const { name, age } = user;
console.log(name); // 'Alice'
console.log(age);  // 25
```

#### 💡 You can also rename:

```javascript
const { name: userName } = user;
console.log(userName); // 'Alice'
```

---

### **4. What is the spread (`...`) and rest operator? How are they different?**

Both use the same syntax (`...`), but they are used in **different contexts**:

#### ✅ Spread operator: **expands** iterable elements

Used in function calls, array/object copies:

```javascript
const arr = [1, 2];
const newArr = [...arr, 3]; // [1, 2, 3]

const obj = { a: 1 };
const newObj = { ...obj, b: 2 }; // { a: 1, b: 2 }
```

#### ✅ Rest operator: **collects** remaining items into an array or object

Used in parameters and destructuring:

```javascript
function sum(...nums) {
  return nums.reduce((a, b) => a + b, 0);
}
sum(1, 2, 3); // 6

const [first, ...rest] = [1, 2, 3];
console.log(rest); // [2, 3]
```

---

### **5. What are generators and when would you use them?**

**Generators** are special functions that can be **paused and resumed**, allowing you to control the flow of data.

Defined using `function*` and use the `yield` keyword.

#### ✅ Example:

```javascript
function* counter() {
  yield 1;
  yield 2;
  yield 3;
}

const gen = counter();
console.log(gen.next().value); // 1
console.log(gen.next().value); // 2
console.log(gen.next().value); // 3
```

#### 🔍 Use Cases:

* Lazy iteration over large or infinite data sets
* Custom iterators
* Pausing function execution (similar to coroutines)
* Asynchronous flow control (with `yield` and `async generators`)

---

Let me know if you'd like these turned into flashcards, a quiz, or a PDF for easy review.
