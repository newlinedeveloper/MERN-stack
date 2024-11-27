### **React Core Concepts**
1. **Explain how reconciliation works in React.**  
2. **What is the purpose of `useMemo` and `useCallback`? How do they differ?**  
3. **How does React's `useEffect` cleanup work? Provide an example.**  
4. **What are the differences between class components and functional components? Why prefer one over the other?**  
5. **How does React handle key prop changes in a list? Why are keys important?**

---

### **Performance Optimization**
6. **How do you optimize React performance in a large-scale application?**  
7. **What are React.memo and React.PureComponent? When would you use them?**  
8. **How do you prevent unnecessary re-renders in React components?**  
9. **What strategies can you use to reduce the size of a React bundle?**  
10. **Explain the impact of using inline functions in React components. How can this be mitigated?**

---

### **State Management**
11. **How do you manage complex states with the `useReducer` hook? Can you compare it to Redux?**  
12. **What are the pros and cons of Context API compared to external state management libraries like Redux or MobX?**  
13. **How do you structure and organize a large global state in a React application?**  
14. **Can you describe the difference between local, global, and derived state? How do you handle them?**

---

### **React Router**
15. **How would you implement protected routes in React Router?**  
16. **Explain the difference between `useNavigate` and `useHistory`. When would you use each?**  
17. **How do you handle deep linking in a React application?**  
18. **What challenges can arise when using dynamic routing with large datasets?**

---

### **Hooks**
19. **How does React handle closure with hooks like `useState` and `useEffect`?**  
20. **What are custom hooks? Can you give an example of one you’ve implemented?**  
21. **Explain the "Rules of Hooks." Why are they important?**  
22. **How would you debounce or throttle input in a functional component using hooks?**

---

### **Testing**
23. **How do you write unit tests for React components using Jest and React Testing Library?**  
24. **What challenges arise when testing components with asynchronous data fetching? How do you solve them?**  
25. **How do you mock React Context values in a test?**  
26. **What are snapshot tests? When are they useful, and what are their limitations?**

---

### **Styling**
27. **Compare CSS-in-JS libraries like Styled-Components and Emotion with traditional CSS. What are the trade-offs?**  
28. **How do you handle dynamic styling in a large React application?**  
29. **What are CSS modules? How do they compare to other styling methods?**  

---

### **Miscellaneous**
30. **How does React handle server-side rendering (SSR) with libraries like Next.js? What are the benefits of SSR?**  
31. **Explain the concept of a "higher-order component" (HOC) and how it compares to React hooks.**  
32. **What is the virtual DOM? How does it differ from the real DOM?**  
33. **What are lazy loading and code splitting? How do they work in React?**  
34. **What are React Portals? When would you use them?**  
35. **Explain how you would handle accessibility (a11y) in a React application.**

---

### Behavioral/Scenario-Based Questions
36. **Describe a challenging React bug you encountered and how you solved it.**  
37. **How have you handled migrating a legacy React application to use modern features like hooks or functional components?**  
38. **What steps would you take to ensure a React application is secure?**  
39. **Have you worked on a React project with real-time features like WebSockets? How did you implement it?**  
40. **How do you handle internationalization (i18n) in React applications?**

---

If you'd like detailed answers or practice on specific questions, let me know!

### **React Core Concepts**

1. **Explain how reconciliation works in React.**  
   Reconciliation is the process React uses to update the DOM efficiently. When a component’s state or props change, React creates a new virtual DOM tree. It then compares it with the previous virtual DOM tree (diffing algorithm). Changes (differences) are calculated, and only those parts of the real DOM are updated, ensuring optimal performance.

2. **What is the purpose of `useMemo` and `useCallback`? How do they differ?**  
   - `useMemo` is used to memoize the result of a computation, avoiding expensive recalculations on every render.  
   - `useCallback` is used to memoize a function, ensuring it doesn't get recreated on every render.  
   - **Difference**: `useMemo` returns a value, while `useCallback` returns a memoized function.

3. **How does React's `useEffect` cleanup work? Provide an example.**  
   Cleanup functions are executed when the component unmounts or before the next effect is run.  
   ```jsx
   useEffect(() => {
       const timer = setInterval(() => console.log('Tick'), 1000);
       return () => clearInterval(timer); // Cleanup
   }, []);
   ```

4. **What are the differences between class components and functional components? Why prefer one over the other?**  
   - **Class Components**: Use lifecycle methods (`componentDidMount`, `shouldComponentUpdate`), `this` keyword, and were the traditional way to manage state.  
   - **Functional Components**: Use hooks for state and lifecycle management, are more concise, and avoid pitfalls of `this`.  
   - **Preference**: Functional components are modern, easier to read, and enable better optimization and reuse (via hooks).

5. **How does React handle key prop changes in a list? Why are keys important?**  
   React uses keys to identify which elements in a list have changed, been added, or removed. Keys should be unique and stable for each item. Changing keys forces React to re-render the component completely, so they should be managed carefully.

---

### **Performance Optimization**

6. **How do you optimize React performance in a large-scale application?**  
   - Use memoization (`useMemo`, `useCallback`).
   - Implement lazy loading and code splitting.  
   - Optimize rendering with React.memo.  
   - Use efficient algorithms for state updates.  
   - Reduce unnecessary re-renders by properly managing props and state.

7. **What are React.memo and React.PureComponent? When would you use them?**  
   - `React.memo`: Prevents functional components from re-rendering if props don’t change.  
   - `React.PureComponent`: Used in class components to perform shallow comparison of props and state.  
   - **Usage**: Use these when components have large subtrees or expensive computations that don’t depend on frequently changing props.

8. **How do you prevent unnecessary re-renders in React components?**  
   - Use `React.memo` or `PureComponent`.  
   - Memoize callbacks with `useCallback`.  
   - Avoid passing new object/array literals directly in props.  
   - Split large components into smaller ones.

9. **What strategies can you use to reduce the size of a React bundle?**  
   - Use dynamic imports for code splitting.  
   - Tree-shaking to remove unused code.  
   - Use smaller libraries or remove unused dependencies.  
   - Minify and compress assets using tools like Terser or Webpack plugins.

10. **Explain the impact of using inline functions in React components. How can this be mitigated?**  
   Inline functions create a new reference on every render, potentially causing child components to re-render.  
   - **Mitigation**: Use `useCallback` or define functions outside render scope to reuse references.

---

### **State Management**

11. **How do you manage complex states with the `useReducer` hook? Can you compare it to Redux?**  
   - `useReducer` is suitable for managing state within a single component or local state logic.  
   - Redux is better for global state, especially in large applications with multiple slices of state.  
   - Example of `useReducer`:  
     ```jsx
     const initialState = { count: 0 };
     const reducer = (state, action) => {
         switch (action.type) {
             case 'increment': return { count: state.count + 1 };
             case 'decrement': return { count: state.count - 1 };
             default: return state;
         }
     };
     const [state, dispatch] = useReducer(reducer, initialState);
     ```

12. **What are the pros and cons of Context API compared to external state management libraries like Redux or MobX?**  
   - **Pros**:  
     - Built-in to React.  
     - Simple and doesn’t require additional dependencies.  
   - **Cons**:  
     - Not suitable for deeply nested state or complex updates.  
     - Causes re-renders in all consuming components.  
   - Use libraries like Redux for better performance and scalability.

13. **How do you structure and organize a large global state in a React application?**  
   - Use a modular approach (e.g., slices in Redux).  
   - Use separate contexts for distinct areas of state.  
   - Normalize data structures to avoid nested state.

14. **Can you describe the difference between local, global, and derived state? How do you handle them?**  
   - **Local state**: Managed within a component (e.g., `useState`).  
   - **Global state**: Shared across multiple components (e.g., Context API, Redux).  
   - **Derived state**: Computed based on existing state (e.g., filtering or sorting).  
   - Handle derived state by computing it on-the-fly in render methods or memoizing results.

---
### **React Router**

15. **How would you implement protected routes in React Router?**  
   Use a wrapper component to check authentication and conditionally render the route:  
   ```jsx
   const ProtectedRoute = ({ children }) => {
       const isAuthenticated = /* check auth logic */;
       return isAuthenticated ? children : <Navigate to="/login" />;
   };
   ```

16. **Explain the difference between `useNavigate` and `useHistory`. When would you use each?**  
   - `useHistory` was used in React Router v5 to navigate programmatically.  
   - `useNavigate` is its replacement in React Router v6, offering a simpler API.  
     ```jsx
     const navigate = useNavigate();
     navigate('/path'); // v6
     ```

17. **How do you handle deep linking in a React application?**  
   Ensure the app handles URL parameters and query strings:  
   ```jsx
   const { id } = useParams(); // Extract URL parameters
   const query = new URLSearchParams(useLocation().search); // Extract query strings
   ```

18. **What challenges can arise when using dynamic routing with large datasets?**  
   - Performance issues with rendering large lists.  
   - URL length limitations if passing large data.  
   - SEO challenges if the content is dynamically fetched.  
   - Solutions include pagination, server-side rendering (SSR), or pre-fetching data.

---

### **Hooks**

19. **How does React handle closure with hooks like `useState` and `useEffect`?**  
   Hooks capture values from their scope when defined, not when executed.  
   ```jsx
   useEffect(() => {
       console.log(count); // Captures `count` from when the effect was defined
   }, []);
   ```

20. **What are custom hooks? Can you give an example of one you’ve implemented?**  
   Custom hooks encapsulate reusable logic. Example:  
   ```jsx
   const useFetch = (url) => {
       const [data, setData] = useState(null);
       useEffect(() => {
           fetch(url).then(res => res.json()).then(setData);
       }, [url]);
       return data;
   };
   ```

21. **Explain the "Rules of Hooks." Why are they important?**  
   - **Rules**:  
     - Call hooks only at the top level (not inside loops, conditions, or nested functions).  
     - Call hooks only in React functions or custom hooks.  
   - These rules ensure consistent behavior and maintain the correct state during renders.

22. **How would you debounce or throttle input in a functional component using hooks?**  
   Example debounce with `useEffect`:  
   ```jsx
   const [value, setValue] = useState('');
   useEffect(() => {
       const handler = setTimeout(() => {
           console.log(value); // Perform action
       }, 500);
       return () => clearTimeout(handler); // Cleanup on change
   }, [value]);
   ```

---

### **Testing**

23. **How do you write unit tests for React components using Jest and React Testing Library?**  
   Example: Testing a button click:  
   ```jsx
   render(<Button onClick={mockFn}>Click Me</Button>);
   fireEvent.click(screen.getByText('Click Me'));
   expect(mockFn).toHaveBeenCalled();
   ```

24. **What challenges arise when testing components with asynchronous data fetching? How do you solve them?**  
   - Challenge: Timing issues with async updates.  
   - Solution: Use `waitFor` or mock async functions:  
     ```jsx
     render(<Component />);
     await waitFor(() => expect(screen.getByText('Loaded')).toBeInTheDocument());
     ```

25. **How do you mock React Context values in a test?**  
   Wrap the component with a mock provider:  
   ```jsx
   render(
       <MyContext.Provider value={mockValue}>
           <Component />
       </MyContext.Provider>
   );
   ```

26. **What are snapshot tests? When are they useful, and what are their limitations?**  
   Snapshot tests compare the rendered output of a component to a saved snapshot.  
   - **Useful**: Detecting unintended UI changes.  
   - **Limitations**: Cannot verify functionality or dynamic behavior.

---

### **Styling**

27. **Compare CSS-in-JS libraries like Styled-Components and Emotion with traditional CSS. What are the trade-offs?**  
   - **CSS-in-JS**: Scoped styles, dynamic theming, and easier maintainability but adds runtime overhead.  
   - **Traditional CSS**: Better performance but lacks scoping and reusability without tools like CSS modules.

28. **How do you handle dynamic styling in a large React application?**  
   - Use CSS-in-JS for dynamic theming.  
   - Separate style logic using utility functions or hooks (e.g., `useTheme`).

29. **What are CSS modules? How do they compare to other styling methods?**  
   CSS Modules allow local scoping by default. They’re simpler and lightweight compared to CSS-in-JS but lack the dynamism of runtime styles.

---

### **Miscellaneous**

30. **How does React handle server-side rendering (SSR) with libraries like Next.js? What are the benefits of SSR?**  
   - SSR generates HTML on the server, improving SEO and initial load time.  
   - Next.js provides `getServerSideProps` to fetch data during SSR.

31. **Explain the concept of a "higher-order component" (HOC) and how it compares to React hooks.**  
   - HOCs wrap components to add functionality, while hooks allow you to share logic directly in components.  
   - Hooks are simpler and avoid the "wrapper hell" associated with HOCs.

32. **What is the virtual DOM? How does it differ from the real DOM?**  
   - The virtual DOM is a lightweight representation of the real DOM.  
   - React updates the virtual DOM first and applies only the differences (diffing) to the real DOM.

33. **What are lazy loading and code splitting? How do they work in React?**  
   - Lazy loading loads components or data only when needed.  
   - Code splitting splits the bundle into smaller chunks.  
     ```jsx
     const LazyComponent = React.lazy(() => import('./Component'));
     ```

34. **What are React Portals? When would you use them?**  
   Portals allow rendering a component outside its parent DOM hierarchy. Useful for modals or tooltips:  
   ```jsx
   ReactDOM.createPortal(<Modal />, document.getElementById('modal-root'));
   ```

35. **Explain how you would handle accessibility (a11y) in a React application.**  
   - Use semantic HTML elements (e.g., `<button>`, `<header>`).  
   - Add ARIA attributes when necessary.  
   - Test with screen readers and tools like Axe.

---

### **Behavioral/Scenario-Based Questions**

36. **Describe a challenging React bug you encountered and how you solved it.**  
   *(Example)*: Debugging a React component that re-rendered excessively due to new inline functions in props. Solved using `useCallback` to memoize functions.

37. **How have you handled migrating a legacy React application to use modern features like hooks or functional components?**  
   - Migrate incrementally.  
   - Replace lifecycle methods with hooks like `useEffect`.  
   - Refactor one component at a time.

38. **What steps would you take to ensure a React application is secure?**  
   - Sanitize user inputs to prevent XSS.  
   - Use HTTPS and secure cookies.  
   - Avoid storing sensitive data in the frontend.

39. **Have you worked on a React project with real-time features like WebSockets? How did you implement it?**  
   - Use libraries like `socket.io-client` or the native WebSocket API.  
   - Manage WebSocket connection state using `useEffect` and `useRef`.

40. **How do you handle internationalization (i18n) in React applications?**  
   - Use libraries like `react-i18next` for translations.  
   - Store translations in JSON files and dynamically load them.

---
