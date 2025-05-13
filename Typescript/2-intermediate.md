Certainly! Here's a complete and concise explanation for each of the **intermediate TypeScript questions related to functions and classes**:

---

### **1. How do you type a function in TypeScript?**

**Answer:**
You can type a function by specifying the types of parameters and the return value.

```ts
function add(a: number, b: number): number {
  return a + b;
}
```

You can also use **function types**:

```ts
type MathOperation = (x: number, y: number) => number;

const multiply: MathOperation = (x, y) => x * y;
```

---

### **2. What is the difference between `interface` and `type` for function signatures?**

Both can define function types, but `interface` is better for **object shapes** and supports declaration merging.

#### **With `type`:**

```ts
type Greet = (name: string) => string;
```

#### **With `interface`:**

```ts
interface Greet {
  (name: string): string;
}
```

* Use `type` if you're composing with unions, intersections, or primitives.
* Use `interface` for object-like structures, especially if you want to extend or merge them.

---

### **3. What are generics in TypeScript? Give an example.**

**Answer:**
Generics allow you to create reusable components or functions that work with **any type**.

```ts
function identity<T>(value: T): T {
  return value;
}

identity<string>("Hello");
identity<number>(42);
```

Generics make code more flexible and type-safe without losing type information.

---

### **4. What is type narrowing? How does TypeScript perform type guards?**

**Answer:**
**Type narrowing** means refining a broader type (like `unknown` or a union) to a more specific one.

**Type Guards** are mechanisms TypeScript uses to narrow types:

* `typeof`
* `instanceof`
* Custom guards

**Example:**

```ts
function print(value: string | number) {
  if (typeof value === "string") {
    console.log(value.toUpperCase()); // value is string
  } else {
    console.log(value.toFixed(2)); // value is number
  }
}
```

**Custom Type Guard:**

```ts
function isString(val: unknown): val is string {
  return typeof val === "string";
}
```

---

### **5. How do enums work in TypeScript?**

**Answer:**
`enum` is a special type that represents a group of named constants.

```ts
enum Direction {
  Up,
  Down,
  Left,
  Right,
}

let dir: Direction = Direction.Up;
```

You can also have **string enums**:

```ts
enum Status {
  Success = "SUCCESS",
  Error = "ERROR",
}
```

Behind the scenes, numeric enums are **reverse-mapped**:

```ts
Direction[0] === "Up"; // true
```

---

### **6. How do you extend interfaces or types?**

**Interfaces:**

```ts
interface Person {
  name: string;
}

interface Employee extends Person {
  salary: number;
}
```

**Types:**

```ts
type Person = {
  name: string;
};

type Employee = Person & {
  salary: number;
};
```

Use `extends` with interfaces, `&` (intersection) with types.

---

### **7. How does `this` behave differently in arrow vs regular functions in TypeScript classes?**

**Answer:**

* **Arrow functions** **capture the `this`** value from their **lexical scope** (where they are defined).
* **Regular functions** have their **own `this`**, which can vary based on how the function is called.

**Example:**

```ts
class Timer {
  count = 0;

  start() {
    setInterval(() => {
      this.count++;
      console.log(this.count); // 'this' refers to Timer
    }, 1000);
  }
}
```

If we used a regular function instead of an arrow function, `this` would be `undefined` or `window` (in strict mode), not the class instance.

---

