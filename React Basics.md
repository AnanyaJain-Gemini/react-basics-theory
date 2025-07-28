# React Basics

### **⦁	Props:** 
Props are read-only inputs that you pass from one component (parent) to another (child) in React.
They allow data to flow downward from parent to child, making your UI dynamic and reusable.
> Props are like parameters to a function

### **⦁	State:** 
It refers to variables or data stored, that can be changed; change in state renders the DOM.
State refers to data that can change over time, like user input or fetched data.

### **⦁	Virtual DOM:** 
The Virtual DOM (VDOM) is a lightweight copy of the real DOM. React uses it to optimize updates: it changes the VDOM first, finds the differences (diffing), and then applies only necessary changes to the actual DOM.

### **⦁	Diffing Algorithm:** 
React compares the old Virtual DOM with the new one; it figures out what changed: added elements, removed elements, or updates to attributes/text/etc; it then creates a list of updates (called **effects**) to apply.

### **⦁	Reconciliation:** 
Reconciliation is the process by which React updates the DOM when the state or props change. It involves diffing the new VDOM tree with the old one and applying the minimum number of changes to the real DOM.
> React does not compare the new VDOM to the real DOM. It only **compares the new VDOM to the old VDOM**, then **updates the real DOM directly based on the diff**.

### **⦁	React Fiber:** 
React Fiber is the reconciliation engine of React (since version 16). It is a complete rewrite of React’s core algorithm that enables incremental rendering, scheduling, and interruption of rendering work.
> It makes rendering interruptible, prioritized, and more efficient. Enables advanced features like concurrent rendering, Suspense, and Transitions.

### **⦁	React Component:** 
Its like a function, that returns an HTML.

### **⦁	Hooks:** 
Hooks are special functions in React that let you use features like **state, lifecycle, or context** in functional components. Whenever you want to make any changes to the UI, like show or reflect any state change to the UI.

#### **1.	`useState` Hook - To Add State** 
`useState` allows your component to **remember values** (like user input, counters, etc.).

#### **2.	`useCallback` Hook - To Memoize Functions:** 
`useCallback` is a React Hook that lets you cache (or remembers) a **function definition** between re-renders. It memorizes a function, so it’s not recreated on every render unless its dependencies change.

```js
// const cachedFn = useCallback(fn, [dependencies])

const handleClick = useCallback(() => {
  console.log("clicked");
}, []); // function is created once; only defined once

const handleClick = useCallback(() => {
  console.log("clicked");
}, [var]); // recreated when "var" changes

const handleClick = useCallback(() => {
  console.log("clicked");
}); // recreated on every render; same as not using "useCallback"

```

#### **3.	`useMemo` Hook - To Memoize Calculations** 
`useMemo` memoizes a value/result, like expensive calculations.
```js
const memoizedValue = useMemo(() => {
  return computeExpensiveValue(input);
}, [input]);  // Recomputes when input changes

const memoizedValue = useMemo(() => {
  return computeExpensiveValue(input);
}, []);  // Computes once

const memoizedValue = useMemo(() => {
  return computeExpensiveValue(input);
});  // Recomputes every render
```

#### **4.	`useRef` Hook - To Store Mutable Values** 
`useRef` stores a reference to a value or DOM element that doesn’t trigger re-renders.

#### **5.	`useEffect` Hook - To Run Side Effects** 
`useEffect` lets you run code after a render — like fetching data, setting up timers, subscriptions, etc. It’s great for side-effects like API calls, logging, or timers.

```js
useEffect(() => {
  console.log("Runs only once when the component mounts");
}, []);

useEffect(() => {
  console.log("Runs on mount + when count changes");
}, [count]);

useEffect(() => {
  console.log("Runs every time i.e. after every render");  // rarely used
}); // no dependencies

```
> Imagine turning on a fan after entering a room. You don't turn it on while entering, but immediately after.
```js
useEffect(() => {
// this will run only once when the component mounts
  const timer = setInterval(() => {
    console.log("tick");
  }, 1000);

  return () => {
// this will run immediately before the component unmounts
    clearInterval(timer); // cleanup
  };
}, []);


const [count, setCount] = useState(0);
  useEffect(() => {
// this will run firstly when the component mounts and then everytime "count" changes
    console.log("Effect runs with count =", count);

    return () => {
// this will run each time "BEFORE" a new component mounts
// this will run before the next effect when "count" changes, or before the component unmounts
      console.log("Cleanup runs with count =", count);
    };
  }, [count]);

```
#### **The Flow of `useEffect()`:**
React **renders first**, and after the DOM has updated, it runs the **cleanup from the previous effect**, then the **new effect.** 
```jsx
Render with count = 0
Effect
Render with count = 1
Cleanup   ← before effect
Effect
Render with count = 2
Cleanup   ← before effect
Effect
Component unmounts
Cleanup   ← before removal
```
> `useEffect` always runs after render. Cleanup from previous effect also runs after render, before the new effect runs
