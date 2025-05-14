Here are detailed explanations with examples for each **Asynchronous JavaScript** question:

---

### **1. Explain `async` / `await`. How is it better than Promises?**

#### ✅ `async` / `await`:

* `async` makes a function return a **promise**.
* `await` pauses the function until the promise is resolved or rejected.
* Introduced in ES2017 (ES8).

#### ✅ Example using Promises:

```javascript
function getData() {
  return fetch('/api/data')
    .then(res => res.json())
    .then(data => console.log(data))
    .catch(err => console.error(err));
}
```

#### ✅ Same with `async/await`:

```javascript
async function getData() {
  try {
    const res = await fetch('/api/data');
    const data = await res.json();
    console.log(data);
  } catch (err) {
    console.error(err);
  }
}
```

#### 🔍 Why is it better?

* Cleaner, more readable code (like synchronous code).
* Easier to write and maintain, especially with `try/catch` error handling.
* Avoids "callback hell" and deep nesting.

---

### **2. What happens if you `await` a non-promise?**

If you `await` a **non-promise**, JavaScript wraps it in a **resolved promise** automatically.

#### ✅ Example:

```javascript
async function demo() {
  const result = await 42;
  console.log(result); // 42
}
demo();
```

#### 🔍 Explanation:

* `await 42` becomes `await Promise.resolve(42)`
* Works fine and returns the value immediately.

---

### **3. How would you handle multiple asynchronous requests in parallel and wait for all of them?**

Use `Promise.all` to run async operations in **parallel** and wait for **all** of them to complete.

#### ✅ Example: `Promise.all`

```javascript
const fetchUser = fetch('/api/user');
const fetchPosts = fetch('/api/posts');

Promise.all([fetchUser, fetchPosts])
  .then(async ([userRes, postsRes]) => {
    const user = await userRes.json();
    const posts = await postsRes.json();
    console.log(user, posts);
  })
  .catch(error => console.error('Error:', error));
```

#### 🔍 What if one fails?

* `Promise.all` fails fast — if **any** promise rejects, the entire `Promise.all` rejects.

---

#### ✅ `Promise.race`:

Returns the **first** settled promise (resolved or rejected).

```javascript
Promise.race([
  fetch('/slow-api'),
  fetch('/fast-api')
]).then(result => {
  console.log('First completed:', result);
});
```

---

### **4. What are microtasks and macrotasks?**

JavaScript handles async code through the **event loop**, which processes tasks in two phases:

| Queue Type     | Examples                                                | Executed                                            |
| -------------- | ------------------------------------------------------- | --------------------------------------------------- |
| **Microtasks** | `Promise.then`, `catch`, `finally`, `queueMicrotask`    | **After** current call stack, before next macrotask |
| **Macrotasks** | `setTimeout`, `setInterval`, `setImmediate`, DOM events | After microtasks complete                           |

#### ✅ Example:

```javascript
console.log('1');

setTimeout(() => console.log('setTimeout'), 0); // macrotask
Promise.resolve().then(() => console.log('promise')); // microtask

console.log('2');
```

#### ✅ Output:

```
1
2
promise
setTimeout
```

#### 🔍 Explanation:

* `console.log('1')` and `console.log('2')` run first (sync).
* Microtask (`promise`) runs before any macrotasks.
* `setTimeout` runs after microtasks.

---

