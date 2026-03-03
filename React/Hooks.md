# React – Hooks (Layman Explanation + Examples + Interview Q&A)

## 1. What Are React Hooks? (Simple Explanation)

Hooks are special functions in React that allow you to use state and other React features inside functional components.

Before Hooks:

* Only class components could manage state and lifecycle methods.

After Hooks:

* Functional components can also handle state, lifecycle, side effects, and more.

In simple words:
Hooks give superpowers to functional components.

---

## 2. Why Were Hooks Introduced?

Problems before Hooks:

* Complex class components
* Confusing lifecycle methods
* Difficult to reuse stateful logic

Hooks solve these problems by:

* Making code simpler
* Improving readability
* Allowing logic reuse via custom hooks

---

## 3. Most Important React Hooks

1. useState
2. useEffect
3. useContext
4. useRef
5. useMemo
6. useCallback

Let’s understand the main ones clearly.

---

# 4. useState Hook

## What is useState?

useState allows you to add state to functional components.

### Example

```jsx
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increase</button>
    </div>
  );
}
```

How it works:

* useState(0) sets initial value.
* setCount updates state.
* Component re-renders automatically.

---

# 5. useEffect Hook

## What is useEffect?

useEffect is used for side effects like:

* API calls
* Timers
* Subscriptions
* DOM updates

### Example – API Call

```jsx
import React, { useEffect, useState } from 'react';

function Users() {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    fetch('https://api.example.com/users')
      .then(res => res.json())
      .then(data => setUsers(data));
  }, []);

  return (
    <ul>
      {users.map(user => (
        <li key={user.id}>{user.name}</li>
      ))}
    </ul>
  );
}
```

Important:

* Empty dependency array [] means run only once (like componentDidMount).

---

# 6. useContext Hook

## What is useContext?

Used to access global data without passing props manually at every level.

Example:

```jsx
const ThemeContext = React.createContext('light');

function Child() {
  const theme = React.useContext(ThemeContext);
  return <div>Theme: {theme}</div>;
}
```

---

# 7. useRef Hook

## What is useRef?

Used to:

* Access DOM elements directly
* Store mutable values without re-rendering

Example:

```jsx
function InputFocus() {
  const inputRef = React.useRef();

  return (
    <div>
      <input ref={inputRef} />
      <button onClick={() => inputRef.current.focus()}>
        Focus Input
      </button>
    </div>
  );
}
```

---

# 8. useMemo Hook

## What is useMemo?

Used to optimize performance by memoizing expensive calculations.

Example:

```jsx
const expensiveValue = useMemo(() => {
  return computeHeavyValue(count);
}, [count]);
```

It recalculates only when count changes.

---

# 9. useCallback Hook

## What is useCallback?

Returns a memoized function.

Used to prevent unnecessary re-renders in child components.

Example:

```jsx
const handleClick = useCallback(() => {
  console.log('Clicked');
}, []);
```

---

# 10. Rules of Hooks

1. Only call Hooks at the top level.
2. Only call Hooks inside React functions.

Wrong:

```jsx
if (condition) {
  useState(0);
}
```

Hooks must not be inside loops or conditions.

---

# 11. Custom Hooks

You can create your own reusable Hooks.

Example:

```jsx
function useCounter(initialValue) {
  const [count, setCount] = useState(initialValue);

  const increment = () => setCount(count + 1);

  return { count, increment };
}
```

Now reusable in multiple components.

---

# 12. Interview Questions & Answers

### Q1: What are React Hooks?

Answer:
Hooks are functions that allow functional components to use state and lifecycle features.

---

### Q2: What is useEffect used for?

Answer:
It handles side effects like API calls, subscriptions, and timers.

---

### Q3: Difference between useMemo and useCallback?

Answer:
useMemo memoizes values.
useCallback memoizes functions.

---

### Q4: What are the rules of Hooks?

Answer:
Hooks must be called at the top level and only inside React functions.

---

### Q5: What is a custom Hook?

Answer:
A reusable function that uses one or more built-in Hooks.

---

### Q6: What happens when state updates?

Answer:
Component re-renders and UI updates.

---

# 13. Real-World Example

Imagine an e-commerce site:

* useState → manage cart items
* useEffect → fetch product data
* useContext → manage global theme
* useMemo → optimize price calculation
* useCallback → prevent unnecessary re-renders

Hooks make functional components powerful and clean.

---

# 14. Key Takeaways

* Hooks allow state in functional components.
* useState and useEffect are most common.
* useMemo and useCallback are for performance.
* Follow rules strictly.
* Custom Hooks improve reusability.

---

If preparing for interviews, make sure you can:

* Explain useState and useEffect clearly
* Explain dependency array behavior
* Explain useMemo vs useCallback
* Create a simple custom Hook

Hooks are one of the most important React interview topics.
