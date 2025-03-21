### **React Hooks: Overview & Examples**
React Hooks allow functional components to use state and lifecycle features without needing a class component.

---

## **1. `useState` - Manage State in Functional Components**
- Allows managing local state inside a functional component.

### **Example: Counter App**
```jsx
import React, { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}

export default Counter;
```

---

## **2. `useEffect` - Perform Side Effects in Components**
- Runs side effects like fetching data, DOM manipulation, or event listeners.

### **Example: Fetch Data on Mount**
```jsx
import React, { useState, useEffect } from "react";

function DataFetcher() {
  const [data, setData] = useState([]);

  useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/todos")
      .then((res) => res.json())
      .then((json) => setData(json));

    return () => {
      console.log("Cleanup function called");
    };
  }, []); // Runs once on mount

  return (
    <div>
      <h3>Fetched Data</h3>
      <ul>{data.slice(0, 5).map((item) => <li key={item.id}>{item.title}</li>)}</ul>
    </div>
  );
}

export default DataFetcher;
```

---

## **3. `useContext` - Manage Global State**
- Avoid prop drilling by sharing state across components.

### **Example: Theme Context**
```jsx
import React, { useContext } from "react";

const ThemeContext = React.createContext("light");

function ThemedButton() {
  const theme = useContext(ThemeContext);
  return <button style={{ backgroundColor: theme === "dark" ? "black" : "white" }}>Click Me</button>;
}

function App() {
  return (
    <ThemeContext.Provider value="dark">
      <ThemedButton />
    </ThemeContext.Provider>
  );
}

export default App;
```

---

## **4. `useRef` - Reference DOM Elements or Persist Values**
- Holds a mutable value that does not cause re-renders.

### **Example: Accessing DOM Element**
```jsx
import React, { useRef } from "react";

function InputFocus() {
  const inputRef = useRef(null);

  const handleFocus = () => {
    inputRef.current.focus();
  };

  return (
    <div>
      <input ref={inputRef} type="text" placeholder="Type here" />
      <button onClick={handleFocus}>Focus Input</button>
    </div>
  );
}

export default InputFocus;
```

---

## **5. `useReducer` - Manage Complex State**
- Works like `useState` but better for complex state logic.

### **Example: Counter with Reducer**
```jsx
import React, { useReducer } from "react";

const reducer = (state, action) => {
  switch (action.type) {
    case "increment":
      return { count: state.count + 1 };
    case "decrement":
      return { count: state.count - 1 };
    default:
      return state;
  }
};

function Counter() {
  const [state, dispatch] = useReducer(reducer, { count: 0 });

  return (
    <div>
      <p>Count: {state.count}</p>
      <button onClick={() => dispatch({ type: "increment" })}>+</button>
      <button onClick={() => dispatch({ type: "decrement" })}>-</button>
    </div>
  );
}

export default Counter;
```

---

## **6. `useMemo` - Optimize Performance**
- Memoizes expensive calculations.

### **Example: Expensive Calculation**
```jsx
import React, { useState, useMemo } from "react";

function ExpensiveComponent() {
  const [count, setCount] = useState(0);
  const [number, setNumber] = useState(5);

  const expensiveCalculation = useMemo(() => {
    console.log("Calculating...");
    return number * 2;
  }, [number]);

  return (
    <div>
      <p>Result: {expensiveCalculation}</p>
      <button onClick={() => setCount(count + 1)}>Increment Count ({count})</button>
      <button onClick={() => setNumber(number + 1)}>Increment Number ({number})</button>
    </div>
  );
}

export default ExpensiveComponent;
```

---

## **7. `useCallback` - Memoize Functions**
- Prevents function recreation on re-renders.

### **Example: Memoized Function**
```jsx
import React, { useState, useCallback } from "react";

function Child({ increment }) {
  console.log("Child rendered");
  return <button onClick={increment}>Increment</button>;
}

const MemoizedChild = React.memo(Child);

function Parent() {
  const [count, setCount] = useState(0);

  const increment = useCallback(() => {
    setCount((prev) => prev + 1);
  }, []);

  return (
    <div>
      <p>Count: {count}</p>
      <MemoizedChild increment={increment} />
    </div>
  );
}

export default Parent;
```

---

## **8. `useLayoutEffect` - Runs Before Paint**
- Similar to `useEffect`, but runs **synchronously** after DOM mutations.

### **Example: Logging Element Size**
```jsx
import React, { useState, useRef, useLayoutEffect } from "react";

function LayoutEffectExample() {
  const divRef = useRef(null);
  const [width, setWidth] = useState(0);

  useLayoutEffect(() => {
    setWidth(divRef.current.offsetWidth);
  }, []);

  return <div ref={divRef}>Width: {width}px</div>;
}

export default LayoutEffectExample;
```

---

## **9. `useImperativeHandle` - Customize Ref Handling**
- Allows parent components to control child component refs.

### **Example: Exposing Methods**
```jsx
import React, { useRef, useImperativeHandle, forwardRef } from "react";

const CustomInput = forwardRef((props, ref) => {
  useImperativeHandle(ref, () => ({
    focus: () => {
      inputRef.current.focus();
    },
  }));
  const inputRef = useRef(null);

  return <input ref={inputRef} type="text" />;
});

function App() {
  const inputRef = useRef(null);

  return (
    <div>
      <CustomInput ref={inputRef} />
      <button onClick={() => inputRef.current.focus()}>Focus Input</button>
    </div>
  );
}

export default App;
```

---

## **Summary of React Hooks**
| Hook                | Purpose |
|---------------------|---------|
| `useState`         | Manage state in function components |
| `useEffect`        | Perform side effects (fetching data, event listeners) |
| `useContext`       | Manage global state without prop drilling |
| `useRef`           | Access DOM elements or persist values without re-render |
| `useReducer`       | Manage complex state logic |
| `useMemo`          | Optimize expensive calculations |
| `useCallback`      | Memoize functions to prevent re-creation |
| `useLayoutEffect`  | Runs before browser paint (for measurements) |
| `useImperativeHandle` | Customize ref behavior in child components |
