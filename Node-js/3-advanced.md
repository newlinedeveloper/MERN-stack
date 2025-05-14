Here’s a detailed answer and explanation for each of the **Advanced Node.js topics** you mentioned—these are often discussed in senior-level interviews and system design rounds:

---

### **1. What is clustering in Node.js and when would you use it?**

* **Clustering** allows you to **fork multiple Node.js processes** to take advantage of **multi-core CPUs**.
* Each process (called a worker) runs an instance of your app and can handle requests independently.
* You use it when you need **horizontal scaling** of your application on a single machine.

#### Example:

```js
const cluster = require('cluster');
const http = require('http');
const os = require('os');

if (cluster.isMaster) {
  const numCPUs = os.cpus().length;
  console.log(`Master ${process.pid} is running`);

  for (let i = 0; i < numCPUs; i++) {
    cluster.fork();
  }

  cluster.on('exit', (worker) => {
    console.log(`Worker ${worker.process.pid} died`);
  });
} else {
  http.createServer((req, res) => {
    res.end(`Handled by worker ${process.pid}`);
  }).listen(3000);

  console.log(`Worker ${process.pid} started`);
}
```

---

### **2. How do you scale a Node.js application?**

* **Vertical scaling**: Increase resources (CPU, RAM) on a single server.
* **Horizontal scaling**:

  * Use **clustering** (as above) for multi-core support.
  * Deploy multiple instances behind a **load balancer** (e.g., Nginx or AWS ELB).
  * Use **containers** (Docker, Kubernetes) for orchestrated deployments.
  * Use **message queues** (e.g., RabbitMQ, Kafka) for decoupling microservices.

---

### **3. How do you implement caching in a Node.js API (e.g., using Redis)?**

Caching improves performance and reduces redundant processing or API/database calls.

* **In-memory caching**: `node-cache`, `lru-cache` for simple cases.
* **Distributed caching**: Use **Redis** to cache across multiple instances.

#### Example with Redis:

```js
const redis = require('redis');
const client = redis.createClient();

app.get('/user/:id', async (req, res) => {
  const { id } = req.params;

  client.get(id, async (err, data) => {
    if (data) {
      return res.send(JSON.parse(data));
    }

    const user = await getUserFromDB(id);
    client.setex(id, 3600, JSON.stringify(user)); // cache for 1 hour
    res.send(user);
  });
});
```

---

### **4. What is event-driven architecture? How does Node.js leverage it?**

* **Event-driven architecture** (EDA) is a software pattern where components **communicate through events**.
* Node.js uses **event-driven, non-blocking I/O**, making it ideal for handling many concurrent operations without multi-threading.

#### Example:

```js
const EventEmitter = require('events');
const emitter = new EventEmitter();

emitter.on('data_received', (data) => {
  console.log('Data:', data);
});

emitter.emit('data_received', { id: 1, name: 'John' });
```

* **Benefit**: Decouples components, improves scalability, ideal for real-time apps (e.g., chat, streaming).

---

### **5. What are worker threads and when should you use them over child processes?**

* **Worker Threads**:

  * Introduced in Node.js v10.5+ for **multi-threading in JS**.
  * Used for **CPU-intensive tasks** (e.g., image processing, encryption).
  * Share memory using `SharedArrayBuffer`.

* **Child Processes**:

  * Use `spawn`, `exec`, or `fork`.
  * Best for **running separate scripts** or processes.
  * Communicate via IPC.

#### When to use:

* Use **worker threads** for **in-process, high-performance parallelism**.
* Use **child processes** to **run isolated, potentially untrusted code** or separate Node apps.

---

### **6. How do you handle memory leaks in Node.js?**

* **Memory leaks** happen when memory is no longer needed but not released.
* Common causes:

  * Global variables
  * Closures holding references
  * Unremoved event listeners
  * Caching too much data

#### Techniques to identify:

* Use `--inspect` with Chrome DevTools.
* Use **heap snapshots** and **`process.memoryUsage()`**.
* Use profiling tools like **clinic.js**, **Valgrind**, or **Heapdump**.

---

### **7. How do you secure a Node.js application against common web vulnerabilities (XSS, CSRF, injection attacks)?**

* **XSS (Cross-site scripting)**:

  * Sanitize user input using libraries like `DOMPurify`.
  * Use `helmet` middleware to set secure headers.

* **CSRF (Cross-site request forgery)**:

  * Use anti-CSRF tokens (e.g., with `csurf` middleware).
  * Enable **SameSite cookies**.

* **Injection attacks**:

  * Use parameterized queries with DBs (e.g., `pg`, `mongoose`).
  * Validate inputs with libraries like `Joi` or `zod`.

* **Other protections**:

  * Rate limiting (`express-rate-limit`)
  * Secure headers (`helmet`)
  * Input validation
  * Avoid `eval()` and unsafe serialization

---

### **8. How does Node.js handle backpressure in streams?**

* **Backpressure** occurs when a writable stream cannot handle the incoming data fast enough from a readable stream.
* Node.js handles it by using the `.write()` method's return value and `.pause()`/`.resume()`:

#### Example:

```js
const fs = require('fs');
const readable = fs.createReadStream('largefile.txt');
const writable = fs.createWriteStream('output.txt');

readable.on('data', (chunk) => {
  const canWrite = writable.write(chunk);
  if (!canWrite) {
    readable.pause(); // backpressure: stop reading
  }
});

writable.on('drain', () => {
  readable.resume(); // resume once writable is ready
});
```

* Proper stream management ensures that the app doesn’t crash or overload memory when writing/reading large files.

---

