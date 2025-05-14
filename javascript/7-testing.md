Here are strong, interview-ready answers to **Testing and Tooling** questions in JavaScript, especially for frontend and fullstack roles:

---

### **1. How would you write unit tests for a JavaScript function?**

Unit tests validate the **smallest testable units** (e.g. functions) to ensure they work as expected.

#### ✅ Example: Function to test

```javascript
function add(a, b) {
  return a + b;
}
```

#### ✅ Test with Jest:

```javascript
// add.test.js
const { add } = require('./add');

test('adds two numbers', () => {
  expect(add(2, 3)).toBe(5);
});
```

#### ✅ Key Concepts:

* Use **`test()`** or **`it()`** to define test cases
* **`expect()`** is used for assertions
* Place tests in files ending with `.test.js` or `.spec.js`

#### ✅ Good Practices:

* Test both valid and edge cases
* Use clear names like `should return 0 when inputs are negative`

---

### **2. What is the difference between `jest.fn()` and `jest.mock()`?**

| Feature  | `jest.fn()`                       | `jest.mock()`                                  |
| -------- | --------------------------------- | ---------------------------------------------- |
| Purpose  | Create standalone mock function   | Automatically mock entire module or dependency |
| Scope    | Local (single function)           | Global (entire file/module)                    |
| Use Case | Custom spy/mocks for one function | Replace real modules with mocks                |

#### ✅ `jest.fn()` example:

```javascript
const mockCallback = jest.fn(x => x + 1);
[1, 2].map(mockCallback);

expect(mockCallback).toHaveBeenCalledTimes(2);
expect(mockCallback).toHaveBeenCalledWith(1);
```

#### ✅ `jest.mock()` example:

```javascript
// utils.js
export const getData = () => fetch('/data');

// __tests__/app.test.js
jest.mock('../utils', () => ({
  getData: jest.fn(() => Promise.resolve('mocked data'))
}));

import { getData } from '../utils';

test('uses mocked getData', async () => {
  const result = await getData();
  expect(result).toBe('mocked data');
});
```

---

### **3. What linters or formatters do you use? How do they help?**

#### ✅ Common Tools:

* **ESLint** – JavaScript linter
* **Prettier** – Code formatter
* **Stylelint** – For CSS or styled-components

#### ✅ Benefits:

| Tool      | What it does                                                                 |
| --------- | ---------------------------------------------------------------------------- |
| ESLint    | Catches errors (e.g. undefined vars, unused imports) and enforces code style |
| Prettier  | Ensures consistent formatting (spaces, semicolons, etc.)                     |
| Stylelint | Helps enforce consistent CSS styling and rules                               |

#### ✅ Example ESLint rule:

```json
{
  "rules": {
    "no-unused-vars": "warn",
    "eqeqeq": "error"
  }
}
```

#### ✅ Integrations:

* Run via CLI (`eslint src/`)
* Add pre-commit hooks (via `lint-staged`, `husky`)
* Configure in CI pipelines for consistent enforcement

---

### ✅ Summary Table

| Topic         | Key Concept                             | Tools/Methods               |
| ------------- | --------------------------------------- | --------------------------- |
| Unit Testing  | Isolate logic into testable units       | Jest, Mocha, Vitest         |
| `jest.fn()`   | Create inline mock functions and spies  | Local mocking               |
| `jest.mock()` | Auto-mock modules or dependencies       | Useful for APIs, DBs, utils |
| Linting       | Catch syntax errors, enforce rules      | ESLint, Stylelint           |
| Formatting    | Consistent code appearance across teams | Prettier                    |

Let me know if you'd like a sample setup for Jest with TypeScript or ESLint + Prettier config!
