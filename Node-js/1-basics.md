Here are clear answers and explanations to the **Basic / Fundamentals Node.js interview questions**:

---

### **1. What is Node.js? How is it different from traditional server-side platforms like PHP or Java?**

**Answer:**
Node.js is an open-source, cross-platform **JavaScript runtime** built on **Google's V8 engine**. It allows you to run JavaScript code **outside the browser**, mainly for server-side applications.

**Differences from PHP/Java:**

* **Non-blocking I/O**: Node.js uses an **event-driven, asynchronous** model.
* **Single-threaded**: Unlike Java/PHP’s multi-threaded models, Node handles many connections on a single thread via the **event loop**.
* **JavaScript-based**: Same language for frontend and backend.

---

### **2. What is the role of the V8 engine in Node.js?**

**Answer:**
The **V8 engine**, developed by Google, is a **JavaScript engine** that compiles JS directly to native machine code.

**In Node.js:**

* It **executes JavaScript** code outside the browser.
* It's the core engine that **powers Node.js performance**, making it fast and efficient.

---

### **3. What is the difference between synchronous and asynchronous code in Node.js?**

**Synchronous:**

* Executes code **line by line**.
* Blocks the program until the current operation completes.

**Asynchronous:**

* Allows **non-blocking execution**.
* Operations like file reads or network calls are handled in the background; the program continues running.

```js
// Sync
const data = fs.readFileSync('file.txt');

// Async
fs.readFile('file.txt', (err, data) => {
  // Callback when done
});
```

---

### **4. What are the different types of modules in Node.js?**

**Answer:**

1. **Core modules** – Built-in (e.g., `fs`, `http`, `path`)
2. **Local modules** – User-defined modules (e.g., `require('./myModule')`)
3. **Third-party modules** – Installed via npm (e.g., `express`, `axios`)

---

### **5. What is `require()` and how is it different from `import` in ES Modules?**

**`require()`** is the **CommonJS** syntax, and **`import`** is for **ES Modules (ESM)**.

| Feature         | `require()`                   | `import`                                                          |
| --------------- | ----------------------------- | ----------------------------------------------------------------- |
| Syntax type     | CommonJS                      | ES Modules                                                        |
| Load time       | Synchronously at runtime      | Asynchronously at load time                                       |
| Node.js default | Default until recent versions | Requires `"type": "module"` in `package.json` or `.mjs` extension |

---

### **6. How does the Node.js event loop work?**

**Answer:**
The **event loop** is a core part of Node's **non-blocking architecture**. It allows Node to handle thousands of concurrent connections with a single thread.

#### Flow:

1. Node receives requests and delegates tasks (I/O, network).
2. Long-running tasks (like file access) go to **libuv’s thread pool**.
3. Once completed, **callbacks** are pushed to the **event queue**.
4. The event loop picks up tasks and runs them.

It’s like a **queue system** that constantly checks if there's a callback to execute.

---

### **7. What is a callback? What are its drawbacks and how do Promises or async/await solve them?**

**Callback**:
A function passed as an argument to another function, executed after an operation completes.

```js
fs.readFile('file.txt', (err, data) => {
  if (err) throw err;
  console.log(data);
});
```

**Drawbacks (Callback Hell):**

* Nested structure
* Hard to read/debug
* Error handling becomes messy

**Promises / async-await:**

* **Promises** provide a cleaner alternative using `.then()` and `.catch()`
* **`async/await`** gives a synchronous-looking syntax while still being async.

```js
// Promise
fs.promises.readFile('file.txt')
  .then(data => console.log(data))
  .catch(err => console.error(err));

// async/await
async function readFile() {
  try {
    const data = await fs.promises.readFile('file.txt');
    console.log(data);
  } catch (err) {
    console.error(err);
  }
}
```

---

Let me know if you'd like **diagrams**, real code examples, or deeper dives into any of these concepts!
