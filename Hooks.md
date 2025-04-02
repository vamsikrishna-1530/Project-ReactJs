## **React Hooks: Explanation, Uses, and When to Use Them**  

React Hooks are functions introduced in **React 16.8** that allow developers to use state and other React features in functional components, eliminating the need for class components. They simplify component logic, improve code readability, and enable better code reuse.  

### **Commonly Used React Hooks and Their Uses**  

#### **1. useState()**  
- **Purpose:** Allows adding state to functional components.  
- **Use case:** When you need to manage local state (e.g., form inputs, toggle buttons).  
- **Example:**  
  ```jsx
  import { useState } from "react";

  function Counter() {
    const [count, setCount] = useState(0);
    
    return (
      <div>
        <p>Count: {count}</p>
        <button onClick={() => setCount(count + 1)}>Increment</button>
      </div>
    );
  }
  ```

#### **2. useEffect()**  
- **Purpose:** Handles side effects in a component (e.g., API calls, subscriptions, updating the DOM).  
- **Use case:** When you need to perform data fetching, event listeners, or manipulate the DOM after render.  
- **Example:**  
  ```jsx
  import { useEffect, useState } from "react";

  function FetchData() {
    const [data, setData] = useState([]);

    useEffect(() => {
      fetch("https://jsonplaceholder.typicode.com/posts")
        .then(response => response.json())
        .then(data => setData(data));

    }, []); // Empty dependency array means it runs once on mount

    return <ul>{data.map(item => <li key={item.id}>{item.title}</li>)}</ul>;
  }
  ```

#### **3. useContext()**  
- **Purpose:** Provides a way to pass data down the component tree without prop drilling.  
- **Use case:** When you need global state management (e.g., theme, authentication).  
- **Example:**  
  ```jsx
  import { useContext, createContext } from "react";

  const ThemeContext = createContext("light");

  function ThemeComponent() {
    const theme = useContext(ThemeContext);
    return <p>Current theme: {theme}</p>;
  }
  ```

#### **4. useRef()**  
- **Purpose:** Creates a reference to DOM elements or persistent values without causing re-renders.  
- **Use case:** When you need to access/manipulate a DOM element (e.g., focus an input field).  
- **Example:**  
  ```jsx
  import { useRef } from "react";

  function FocusInput() {
    const inputRef = useRef(null);

    return (
      <div>
        <input ref={inputRef} type="text" />
        <button onClick={() => inputRef.current.focus()}>Focus Input</button>
      </div>
    );
  }
  ```

#### **5. useReducer()**  
- **Purpose:** Manages complex state logic, similar to `useState` but with reducers.  
- **Use case:** When you have a state with multiple sub-values or actions (e.g., form handling, counter logic).  
- **Example:**  
  ```jsx
  import { useReducer } from "react";

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
  ```

#### **6. useMemo()**  
- **Purpose:** Optimizes performance by memoizing values to prevent unnecessary calculations.  
- **Use case:** When you need to cache a computed value to avoid re-computation.  
- **Example:**  
  ```jsx
  import { useMemo, useState } from "react";

  function ExpensiveCalculation({ num }) {
    const computedValue = useMemo(() => {
      console.log("Computing...");
      return num * 2;
    }, [num]);

    return <p>Computed Value: {computedValue}</p>;
  }
  ```

#### **7. useCallback()**  
- **Purpose:** Returns a memoized function to prevent unnecessary re-creations.  
- **Use case:** When passing a function as a prop to child components (useful for optimizing performance).  
- **Example:**  
  ```jsx
  import { useCallback, useState } from "react";

  function ParentComponent() {
    const [count, setCount] = useState(0);

    const handleClick = useCallback(() => {
      console.log("Button clicked!");
    }, []);

    return (
      <div>
        <p>Count: {count}</p>
        <button onClick={() => setCount(count + 1)}>Increment</button>
        <ChildComponent onClick={handleClick} />
      </div>
    );
  }

  function ChildComponent({ onClick }) {
    return <button onClick={onClick}>Click me</button>;
  }
  ```

#### **8. useLayoutEffect()**  
- **Purpose:** Similar to `useEffect`, but runs synchronously after DOM mutations.  
- **Use case:** When you need to measure layout changes before the browser paints (e.g., animations).  
- **Example:**  
  ```jsx
  import { useLayoutEffect, useRef } from "react";

  function LayoutEffectComponent() {
    const divRef = useRef(null);

    useLayoutEffect(() => {
      console.log(divRef.current.getBoundingClientRect());
    }, []);

    return <div ref={divRef}>Measure me!</div>;
  }
  ```

#### **9. useImperativeHandle()**  
- **Purpose:** Customizes the instance value that is exposed when using `ref` in parent components.  
- **Use case:** When you need to control the internal state of a child component from its parent.  
- **Example:**  
  ```jsx
  import { useImperativeHandle, useRef, forwardRef } from "react";

  const Child = forwardRef((props, ref) => {
    useImperativeHandle(ref, () => ({
      alertMessage: () => alert("Hello from child!"),
    }));
    return <p>Child Component</p>;
  });

  function Parent() {
    const childRef = useRef(null);

    return (
      <div>
        <Child ref={childRef} />
        <button onClick={() => childRef.current.alertMessage()}>Alert</button>
      </div>
    );
  }
  ```

---

### **When to Use Hooks?**  
Use Hooks in **functional components** when you need:  
✅ State management (`useState`, `useReducer`)  
✅ Side effects (`useEffect`, `useLayoutEffect`)  
✅ Performance optimizations (`useMemo`, `useCallback`)  
✅ DOM manipulation (`useRef`, `useImperativeHandle`)  
✅ Context data (`useContext`)  

**⚠️ Rules of Hooks:**  
1. **Only call Hooks at the top level** (Don’t use them inside loops, conditions, or nested functions).  
2. **Only call Hooks from React function components** (or custom Hooks).  
