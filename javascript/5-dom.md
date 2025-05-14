Here's a detailed breakdown of **DOM and Browser Environment** concepts and interview-ready answers with examples:

---

### **1. How does event delegation work?**

**Event delegation** is a pattern where a single event listener is added to a **parent element**, and it **handles events** for its child elements using **event bubbling**.

#### ✅ Example:

```html
<ul id="list">
  <li>Item 1</li>
  <li>Item 2</li>
</ul>
```

```javascript
document.getElementById('list').addEventListener('click', function (e) {
  if (e.target.tagName === 'LI') {
    console.log('Clicked:', e.target.textContent);
  }
});
```

#### 🔍 Benefits:

* Fewer event listeners → better performance.
* Handles dynamic elements (added later via JS).
* Easy to manage bubbling events from children.

---

### **2. What is the difference between `e.preventDefault()` and `e.stopPropagation()`?**

| Method              | Purpose                                                              |
| ------------------- | -------------------------------------------------------------------- |
| `preventDefault()`  | Stops default browser behavior (e.g., form submit, link navigation). |
| `stopPropagation()` | Stops the event from bubbling up to parent elements.                 |

#### ✅ Example:

```javascript
document.getElementById('link').addEventListener('click', function (e) {
  e.preventDefault(); // Stops navigation
  e.stopPropagation(); // Stops bubbling to parent
  console.log('Clicked link');
});
```

#### 🔍 Real-world use:

* `preventDefault()` for canceling form submits.
* `stopPropagation()` when you don’t want parent listeners to fire.

---

### **3. What is a memory leak in JavaScript and how can you prevent it?**

A **memory leak** happens when memory that’s no longer needed is **not released**, causing increasing memory usage over time.

#### 🔍 Common causes:

* Unremoved DOM event listeners
* Forgotten global variables
* Closures holding references
* Detached DOM elements

#### ✅ Example (bad):

```javascript
const el = document.getElementById('button');
el.addEventListener('click', function () {
  console.log('Clicked');
});
// If element is removed but listener not cleaned up → leak
```

#### ✅ Prevention:

* Use `removeEventListener` when removing elements
* Avoid global variables
* Nullify references when not needed
* Use modern tools: Chrome DevTools → Memory tab → Heap snapshots

---

### **4. How do debouncing and throttling work?**

Used to **control how often a function is executed**, especially in **performance-sensitive** scenarios like scroll, resize, input events.

---

#### ✅ Debouncing:

* **Delays** function execution until a pause (after X ms of inactivity).
* Good for: Search inputs, resize events.

```javascript
function debounce(fn, delay) {
  let timer;
  return function (...args) {
    clearTimeout(timer);
    timer = setTimeout(() => fn.apply(this, args), delay);
  };
}

window.addEventListener('resize', debounce(() => {
  console.log('Resized');
}, 300));
```

---

#### ✅ Throttling:

* Ensures function runs **at most once per interval**.
* Good for: Scroll, mousemove.

```javascript
function throttle(fn, limit) {
  let inThrottle = false;
  return function (...args) {
    if (!inThrottle) {
      fn.apply(this, args);
      inThrottle = true;
      setTimeout(() => (inThrottle = false), limit);
    }
  };
}

window.addEventListener('scroll', throttle(() => {
  console.log('Scrolling');
}, 500));
```

---

### ✅ Summary Table:

| Concept             | Description                              | Use Case                      |
| ------------------- | ---------------------------------------- | ----------------------------- |
| Event Delegation    | Parent handles child events via bubbling | Lists, dynamic elements       |
| `preventDefault()`  | Cancels default behavior                 | Form submits, link navigation |
| `stopPropagation()` | Stops event from bubbling                | Nested events                 |
| Memory Leak         | Unused memory not released               | Event listeners, DOM refs     |
| Debounce            | Executes after pause                     | Search input, resize          |
| Throttle            | Executes every X ms                      | Scroll, mousemove             |

Let me know if you'd like a visual diagram or cheat sheet for these too!
