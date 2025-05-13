Great questions — these are **senior-level** TypeScript topics that test how well you apply TypeScript to real-world, large-scale applications.

---

### **1. How would you gradually migrate a large JS codebase to TypeScript?**

A **step-by-step, incremental approach** is best.

#### ✅ Strategy:

1. **Initialize TS**

   * Add TypeScript: `npm install --save-dev typescript`
   * Generate `tsconfig.json`: `npx tsc --init`
   * Set `allowJs: true` and `checkJs: true` in `tsconfig.json` to type-check existing JS.

2. **Start with type-checking JS files**

   * Enable JSDoc-style comments.
   * Fix the most critical typing issues.

3. **Rename files to `.ts` / `.tsx` incrementally**

   * Start with leaf modules or utility functions.
   * Slowly move up the dependency tree.

4. **Use `any` where necessary**

   * TypeScript allows `any` to ease the transition.
   * Use `// @ts-ignore` sparingly for known issues.

5. **Introduce stricter compiler options gradually**

   * `noImplicitAny`, `strictNullChecks`, `strictFunctionTypes`, etc.

6. **Automate type checking in CI**

   * Prevent regressions by enforcing `tsc` in build/test pipeline.

---

### **2. How do you deal with third-party JS libraries that don’t have types?**

#### ✅ Strategy:

1. **Check if DefinitelyTyped has types**:

   ```bash
   npm install --save-dev @types/library-name
   ```

2. **If types are not available**, create a custom `.d.ts` file:

   * Example: `types/myLib/index.d.ts`

   ```ts
   declare module 'my-legacy-library' {
     export function myFunc(): void;
   }
   ```

3. **Use `require` or `import as any` as fallback**:

   ```ts
   // Fallback, not ideal
   const myLib = require('my-legacy-library') as any;
   ```

4. **Wrap library access in a typed adapter**:

   * Provides type-safe access while keeping the core untyped.

---

### **3. How do you ensure proper types in APIs (e.g., with Axios or Fetch)?**

Define a shared type or interface for the API response and use it consistently.

#### ✅ With Axios:

```ts
interface User {
  id: string;
  name: string;
}

const fetchUser = async (): Promise<User> => {
  const response = await axios.get<User>("/api/user");
  return response.data;
};
```

#### ✅ With Fetch:

```ts
interface User {
  id: string;
  name: string;
}

const fetchUser = async (): Promise<User> => {
  const res = await fetch("/api/user");
  const data = await res.json();
  return data as User;
};
```

💡 **Bonus tip**: Use **zod**, **yup**, or **io-ts** to validate runtime shapes safely.

---

### **4. How can TypeScript improve refactoring safety in a large app?**

#### ✅ Major benefits:

* **Compile-time errors**: Catch broken references (e.g., renamed methods, changed types).
* **Auto-suggestions**: IDEs provide context-aware autocompletions and refactor tools.
* **Dependency safety**: Rename a function or move a file, and all usages update or fail to compile.
* **Contract enforcement**: Function signatures and interfaces act like contracts between modules.
* **Reduced runtime bugs**: Because mistakes are caught during development.

#### ✅ Example:

```ts
type User = { id: string; name: string };

// Changing name to fullName breaks all dependent code — clearly visible during compile
type User = { id: string; fullName: string };
```

---

