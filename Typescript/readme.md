## ✅ **1. Basic / Fundamentals**

These questions assess your understanding of TypeScript's core features.

* **What is TypeScript and how is it different from JavaScript?**
* **What are the benefits of using TypeScript?**
* **What are the different types available in TypeScript?**

  * `string`, `number`, `boolean`, `any`, `unknown`, `void`, `never`, `null`, `undefined`
* **What is the difference between `any`, `unknown`, and `never`?**
* **What is type inference?**
* **What is a union vs intersection type?**
* **What is type alias vs interface? When do you use each?**
* **How do you make a property optional or readonly in an interface?**
* **What is a tuple in TypeScript?**

---

## ✅ **2. Intermediate / Functions / Classes**

Useful for building reusable components or APIs.

* **How do you type a function in TypeScript?**
* **What is the difference between `interface` and `type` for function signatures?**
* **What are generics in TypeScript? Give an example.**
* **What is type narrowing? How does TypeScript perform type guards?**
* **How do enums work in TypeScript?**
* **How do you extend interfaces or types?**
* **How does `this` behave differently in arrow vs regular functions in TypeScript classes?**

---

## ✅ **3. Advanced / Complex Use Cases**

These test deeper understanding or real-world usage in enterprise codebases.

* **What is `keyof`, `typeof`, `in`, and `infer` in TypeScript?**
* **How would you create a mapped type?**

  ```ts
  type Optional<T> = { [K in keyof T]?: T[K] }
  ```
* **What are conditional types in TypeScript?**
* **Explain utility types like `Partial<T>`, `Pick<T>`, `Omit<T>`, `Record<K, T>`**
* **What is the difference between `interface A {}` and `type A = {}` when extending types?**
* **What is declaration merging in TypeScript?**
* **How do you create custom types for third-party libraries without types?**
* **How do you handle dynamic object keys in TypeScript?**

---

## ✅ **4. React + TypeScript Specific**

If you're using TypeScript with React, these are common.

* **How do you type React component props and state?**
* **How do you type a functional component with `useState`, `useEffect`?**
* **How do you type `useRef`, `useReducer` in TypeScript?**
* **How do you type `children` in a React component?**
* **What is the difference between `React.FC` and manually typing props?**
* **How do you type event handlers in React (e.g., `onChange`, `onClick`) in TypeScript?**

---

## ✅ **5. Tooling / Project Setup**

Related to configuration and ecosystem.

* **What does `tsconfig.json` do? What are important compiler options like `strict`, `esModuleInterop`, `noImplicitAny`?**
* **What is `declaration: true` used for?**
* **How do you configure TypeScript with Babel or Webpack?**
* **How do you add TypeScript to an existing JavaScript project?**

---

## ✅ **6. Real-World Scenarios**

Expect at senior levels.

* **How would you gradually migrate a large JS codebase to TS?**
* **How do you deal with third-party JS libraries that don’t have types?**
* **How do you ensure proper types in APIs (e.g., with Axios or Fetch)?**
* **How can TypeScript improve refactoring safety in a large app?**

---

### 🧠 Pro Tip: Focus on explaining **why** TypeScript improves reliability, how you use it to catch bugs early, and how you balance strict types vs developer productivity.

---

