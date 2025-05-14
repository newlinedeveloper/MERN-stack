Here are clear, well-explained solutions to each **JavaScript Code/Algorithm** interview question you've listed:

---

### **1. Reverse a string in JavaScript**

```javascript
function reverseString(str) {
  return str.split('').reverse().join('');
}

console.log(reverseString("hello")); // "olleh"
```

#### 🔍 Explanation:

* `split('')`: converts string to array of characters
* `reverse()`: reverses the array
* `join('')`: joins back into a string

---

### **2. Flatten a nested array**

#### ✅ Using recursion:

```javascript
function flattenArray(arr) {
  return arr.reduce((acc, val) => 
    Array.isArray(val) ? acc.concat(flattenArray(val)) : acc.concat(val), []);
}

console.log(flattenArray([1, [2, [3, [4]]]])); // [1, 2, 3, 4]
```

#### ✅ ES6 one-liner (if depth is known):

```javascript
console.log([1, [2, [3, [4]]]].flat(Infinity));
```

---

### **3. Write a function to deep clone an object**

#### ✅ Using recursion:

```javascript
function deepClone(obj) {
  if (obj === null || typeof obj !== 'object') return obj;

  if (Array.isArray(obj)) {
    return obj.map(deepClone);
  }

  const cloned = {};
  for (let key in obj) {
    if (obj.hasOwnProperty(key)) {
      cloned[key] = deepClone(obj[key]);
    }
  }
  return cloned;
}

const original = { a: 1, b: { c: 2 } };
const copy = deepClone(original);
copy.b.c = 42;

console.log(original.b.c); // 2
```

> Note: For complex structures (e.g. circular refs), use libraries like `lodash.clonedeep`.

---

### **4. Implement a debounce or throttle function**

#### ✅ Debounce:

```javascript
function debounce(fn, delay) {
  let timer;
  return function (...args) {
    clearTimeout(timer);
    timer = setTimeout(() => fn.apply(this, args), delay);
  };
}

// Usage
window.addEventListener('resize', debounce(() => {
  console.log('Debounced resize event');
}, 300));
```

#### ✅ Throttle:

```javascript
function throttle(fn, limit) {
  let inThrottle;
  return function (...args) {
    if (!inThrottle) {
      fn.apply(this, args);
      inThrottle = true;
      setTimeout(() => inThrottle = false, limit);
    }
  };
}

// Usage
window.addEventListener('scroll', throttle(() => {
  console.log('Throttled scroll event');
}, 200));
```

---

### **5. Group an array of objects by a property**

#### ✅ Example:

```javascript
const people = [
  { name: 'Alice', age: 25 },
  { name: 'Bob', age: 25 },
  { name: 'Eve', age: 30 }
];

function groupBy(arr, key) {
  return arr.reduce((acc, obj) => {
    const group = obj[key];
    acc[group] = acc[group] || [];
    acc[group].push(obj);
    return acc;
  }, {});
}

console.log(groupBy(people, 'age'));
// {
//   25: [{name: 'Alice',...}, {name: 'Bob',...}],
//   30: [{name: 'Eve',...}]
// }
```

---

### **6. Write a custom implementation of `Array.prototype.map`**

```javascript
Array.prototype.myMap = function (callback) {
  const result = [];
  for (let i = 0; i < this.length; i++) {
    // Check if index exists (to skip holes in sparse arrays)
    if (this.hasOwnProperty(i)) {
      result.push(callback(this[i], i, this));
    }
  }
  return result;
};

const nums = [1, 2, 3];
console.log(nums.myMap(x => x * 2)); // [2, 4, 6]
```

#### 🔍 Key Features:

* Works like `.map()`
* Takes a callback with `value, index, array`
* Returns a new array

---

Let me know if you want to practice more algorithm-style questions (e.g. sorting, recursion, trees), or need a PDF/cheatsheet version of these!
