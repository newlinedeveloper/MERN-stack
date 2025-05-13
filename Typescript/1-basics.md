Here are **clear and concise answers** with explanations to the TypeScript basic/fundamental interview questions you've listed:

---

### **1. What is TypeScript and how is it different from JavaScript?**

**Answer:**
TypeScript is a **typed superset of JavaScript** developed by Microsoft that compiles to plain JavaScript. It adds **static type checking**, **interfaces**, **generics**, and **advanced tooling support**, which JavaScript does not natively have.

**Key Differences:**

* TypeScript enforces types at compile time (not runtime).
* JavaScript is dynamically typed; TypeScript is statically typed.
* TypeScript code is transpiled to JavaScript for execution.

---

### **2. What are the benefits of using TypeScript?**

**Answer:**

* Early **bug detection** with static type checking.
* Better **code completion**, **intellisense**, and **refactoring** support.
* Improved **documentation** and **self-descriptive code**.
* Supports **modern JavaScript features** (like ES6+) with backward compatibility.
* Encourages writing **scalable, maintainable code** in large codebases.

---

### **3. What are the different types available in TypeScript?**

**Answer:**
Common built-in types include:

* `string`
* `number`
* `boolean`
* `any` – disables type checking
* `unknown` – similar to `any` but safer (must be type-checked before use)
* `void` – function returns nothing
* `never` – function never returns (e.g., throws an error or infinite loop)
* `null` and `undefined`

---

### **4. What is the difference between `any`, `unknown`, and `never`?**

| Type      | Description                                                                |
| --------- | -------------------------------------------------------------------------- |
| `any`     | Disables type checking completely (unsafe).                                |
| `unknown` | Like `any`, but safer – requires type-checking before use.                 |
| `never`   | Represents a value that never occurs – used in unreachable code or errors. |

**Example:**

```ts
let value: unknown = "hello";
// value.toUpperCase(); ❌ compile error
if (typeof value === "string") {
  console.log(value.toUpperCase()); // ✅ safe
}
```

---

### **5. What is type inference?**

**Answer:**
TypeScript automatically assigns a type to a variable if not explicitly defined.

**Example:**

```ts
let message = "hello"; // inferred as string
message = 123; // ❌ Error: number is not assignable to string
```

---

### **6. What is a union vs intersection type?**

**Answer:**

* **Union (`|`)**: A variable can be one **of several types**.

  ```ts
  let id: string | number;
  id = "abc";
  id = 123;
  ```

* **Intersection (`&`)**: A variable must satisfy **all combined types**.

  ```ts
  type A = { name: string };
  type B = { age: number };
  type Person = A & B; // Must have both name and age
  ```

---

### **7. What is type alias vs interface? When do you use each?**

**Type Alias:**

```ts
type User = {
  name: string;
  age: number;
};
```

**Interface:**

```ts
interface User {
  name: string;
  age: number;
}
```

**Differences:**

* Interfaces are best for **object shapes**, especially with **inheritance/extends**.
* Type aliases can represent **primitives, unions, tuples**, etc.
* Interfaces can be **merged** (declaration merging), type aliases cannot.

**Use interface when** defining object structure.
**Use type when** combining types, using unions/intersections, or for flexibility.

---

### **8. How do you make a property optional or readonly in an interface?**

```ts
interface User {
  readonly id: number;
  name: string;
  age?: number; // optional
}
```

* `readonly` means the property **cannot be reassigned**.
* `?` means the property is **optional**.

---

### **9. What is a tuple in TypeScript?**

**Answer:**
A tuple is a **fixed-length, ordered array** with specific types at each index.

**Example:**

```ts
let user: [string, number];
user = ["Alice", 30]; // ✅
user = [30, "Alice"]; // ❌
```

Tuples can also have optional or rest elements.

---

