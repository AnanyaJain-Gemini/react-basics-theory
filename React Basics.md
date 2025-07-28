# React Basics

**⦁	Hooks:** Whenever you want to make any changes to the UI, like show or reflect any state change to the UI.

**⦁	State:** It refers to variables or data stored, that can be changed; change in state renders the DOM.
State refers to data that can change over time, like user input or fetched data.

**⦁	useCallback Hook:** It is a React Hook that lets you cache a function definition between re-renders.
```js
const cachedFn = useCallback(fn, [dependencies])
```
It memorizes (or remembers) a function, so it’s not recreated on every render unless its dependencies change.

**⦁	React Component:** Its like a function, that returns an HTML.

**⦁	Virtual DOM:** The Virtual DOM (VDOM) is a lightweight copy of the real DOM. React uses it to optimize updates: it changes the VDOM first, finds the differences (diffing), and then applies only necessary changes to the actual DOM.

**⦁	Reconciliation:** Reconciliation is the process by which React updates the DOM when the state or props change. It involves diffing the new VDOM tree with the old one and applying the minimum number of changes to the real DOM.

**⦁	React Fiber:**
