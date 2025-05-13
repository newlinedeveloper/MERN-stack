Certainly! Below are **clear answers and explanations** for **React + TypeScript interview questions** — great for projects using modern React with TypeScript.

---

### **1. How do you type React component props and state?**

For **class components**:

```tsx
type MyProps = {
  title: string;
  count?: number;
};

type MyState = {
  isOpen: boolean;
};

class MyComponent extends React.Component<MyProps, MyState> {
  state: MyState = { isOpen: false };

  render() {
    return <h1>{this.props.title}</h1>;
  }
}
```

For **functional components**:

```tsx
type MyProps = {
  title: string;
};

const MyComponent = ({ title }: MyProps) => <h1>{title}</h1>;
```

---

### **2. How do you type a functional component with `useState`, `useEffect`?**

```tsx
import { useState, useEffect } from "react";

// useState with explicit type
const [count, setCount] = useState<number>(0);

// useEffect - no extra typing needed in most cases
useEffect(() => {
  console.log("Effect runs");
}, []);
```

You can use union types too:

```ts
const [value, setValue] = useState<string | null>(null);
```

---

### **3. How do you type `useRef`, `useReducer` in TypeScript?**

#### ✅ `useRef` (for DOM element or value):

```tsx
import { useRef } from "react";

// For value storage
const timerRef = useRef<number | null>(null);

// For DOM elements
const inputRef = useRef<HTMLInputElement>(null);
```

#### ✅ `useReducer`:

```tsx
type State = { count: number };
type Action = { type: "increment" | "decrement" };

const reducer = (state: State, action: Action): State => {
  switch (action.type) {
    case "increment":
      return { count: state.count + 1 };
    case "decrement":
      return { count: state.count - 1 };
    default:
      return state;
  }
};

const [state, dispatch] = useReducer(reducer, { count: 0 });
```

---

### **4. How do you type `children` in a React component?**

#### ✅ Option 1: Using `ReactNode`

```tsx
type Props = {
  children: React.ReactNode;
};

const Wrapper: React.FC<Props> = ({ children }) => <div>{children}</div>;
```

#### ✅ Option 2: With `React.PropsWithChildren`

```tsx
type CardProps = {
  title: string;
};

const Card: React.FC<React.PropsWithChildren<CardProps>> = ({ title, children }) => (
  <div>
    <h2>{title}</h2>
    {children}
  </div>
);
```

---

### **5. What is the difference between `React.FC` and manually typing props?**

| Feature             | `React.FC`                      | Manual Props Typing              |
| ------------------- | ------------------------------- | -------------------------------- |
| Implicit `children` | ✅ Included                      | ❌ Must be added explicitly       |
| Return type         | Assumed to return JSX.Element   | You control the return type      |
| Readability         | ✅ Concise, but debated          | ✅ More explicit and preferred    |
| Community usage     | Used less now (except for HOCs) | Preferred by maintainers & teams |

```tsx
// Using React.FC
const MyComponent: React.FC<{ name: string }> = ({ name }) => <div>{name}</div>;

// Manual typing
type Props = { name: string };
const MyComponent = ({ name }: Props) => <div>{name}</div>;
```

---

### **6. How do you type event handlers in React (e.g., `onChange`, `onClick`) in TypeScript?**

React uses **SyntheticEvent**, and you can type events precisely based on the element.

```tsx
// onClick for a button
const handleClick = (e: React.MouseEvent<HTMLButtonElement>) => {
  console.log("Clicked");
};

// onChange for input
const handleChange = (e: React.ChangeEvent<HTMLInputElement>) => {
  console.log(e.target.value);
};

// onSubmit for a form
const handleSubmit = (e: React.FormEvent<HTMLFormElement>) => {
  e.preventDefault();
};
```

---

