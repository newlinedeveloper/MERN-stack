Here are **clear and concise explanations and examples** for each of the **Advanced / Complex TypeScript interview questions**, often seen in enterprise-grade codebases:

---

### **1. What is `keyof`, `typeof`, `in`, and `infer` in TypeScript?**

#### ✅ `keyof`

Returns a **union of property names** of a given type.

```ts
type Person = { name: string; age: number };
type PersonKeys = keyof Person; // "name" | "age"
```

#### ✅ `typeof`

Used to extract the type of a variable.

```ts
const user = { name: "Alice", age: 30 };
type User = typeof user; // same shape as the object
```

#### ✅ `in`

Used in **mapped types** to iterate over keys.

```ts
type Optional<T> = { [K in keyof T]?: T[K] };
```

#### ✅ `infer`

Used within conditional types to **infer** a type from another.

```ts
type ReturnType<T> = T extends (...args: any[]) => infer R ? R : never;
```

---

### **2. How would you create a mapped type?**

**Mapped types** transform each property in a type using `in` and `keyof`.

```ts
type Readonly<T> = {
  readonly [K in keyof T]: T[K];
};
```

Another example – making all properties optional:

```ts
type Optional<T> = {
  [K in keyof T]?: T[K];
};
```

---

### **3. What are conditional types in TypeScript?**

Conditional types allow you to express **logic based on types**:

```ts
type IsString<T> = T extends string ? "Yes" : "No";

type A = IsString<string>; // "Yes"
type B = IsString<number>; // "No"
```

They can be combined with `infer` for advanced type computations.

---

### **4. Explain utility types like `Partial<T>`, `Pick<T>`, `Omit<T>`, `Record<K, T>`**

| Utility        | Description                                                                       |
| -------------- | --------------------------------------------------------------------------------- |
| `Partial<T>`   | Makes all properties optional. `Partial<{a: string}>` → `{ a?: string }`          |
| `Pick<T, K>`   | Selects specific properties. `Pick<User, 'name'>` → `{ name: string }`            |
| `Omit<T, K>`   | Excludes specific properties. `Omit<User, 'age'>` → `{ name: string }`            |
| `Record<K, T>` | Constructs a type with keys `K` and values `T`. Example: `Record<string, number>` |

---

### **5. What is the difference between `interface A {}` and `type A = {}` when extending types?**

| Feature           | `interface`           | `type`                               |
| ----------------- | --------------------- | ------------------------------------ |
| Extendable        | Yes (`extends`)       | Yes (via intersections: `&`)         |
| Declaration Merge | ✅ Supported           | ❌ Not supported                      |
| Flexibility       | Limited (object only) | Versatile (unions, primitives, etc.) |

**Example:**

```ts
interface A { x: number }
interface B extends A { y: string }

type AType = { x: number }
type BType = AType & { y: string }
```

---

### **6. What is declaration merging in TypeScript?**

**Declaration merging** allows multiple `interface` declarations with the same name to be **automatically merged** into one.

```ts
interface User {
  name: string;
}

interface User {
  age: number;
}

// Becomes: { name: string; age: number }
```

⚠️ Only `interfaces` (and `namespaces`) can merge—`type` aliases cannot.

---

### **7. How do you create custom types for third-party libraries without types?**

You can declare **ambient module declarations** in a `.d.ts` file:

```ts
// types/custom.d.ts
declare module 'some-legacy-lib' {
  export function doSomething(input: string): string;
}
```

Then import and use it like a typed module:

```ts
import { doSomething } from 'some-legacy-lib';
```

Or use `declare global` to extend global types.

---

### **8. How do you handle dynamic object keys in TypeScript?**

Use `index signatures` or `Record` types.

```ts
// Index signature
type Config = {
  [key: string]: string;
};

// Record type
type Config = Record<string, string>;
```

For known keys:

```ts
type Theme = "light" | "dark";
type ThemeColors = Record<Theme, string>;
```

---

