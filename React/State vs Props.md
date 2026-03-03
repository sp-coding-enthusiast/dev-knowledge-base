# React – State vs Props (Layman Explanation + Examples + Interview Q&A)

## 1. Simple Introduction

In React, **State** and **Props** are used to manage and pass data inside components.

If you understand this clearly, you understand the foundation of React.

---

# 2. What are Props? (Simple Explanation)

Props (short for properties) are data passed from a parent component to a child component.

In simple words:
Props are like function arguments.

They are:

* Read-only
* Passed from parent to child
* Cannot be modified by child

---

## Props Analogy

Imagine a parent giving lunch to a child.

* Parent decides what to give.
* Child receives it.
* Child cannot change it.

That is how props work.

---

## Props Example

### Parent Component

```jsx
function Parent() {
  return <Child name="Saurabh" />;
}
```

### Child Component

```jsx
function Child(props) {
  return <h1>Hello {props.name}</h1>;
}
```

Output:
Hello Saurabh

Important:
Child cannot modify props.name.

---

# 3. What is State? (Simple Explanation)

State is data that belongs to a component and can change over time.

In simple words:
State is a component’s internal memory.

It is:

* Mutable (can change)
* Controlled by the component itself
* Causes re-render when updated

---

## State Analogy

Imagine a person’s mood.

* Mood belongs to the person.
* It can change.
* When mood changes, behavior changes.

State works the same way.

---

## State Example

```jsx
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>
        Increase
      </button>
    </div>
  );
}
```

When button is clicked:

* State updates
* Component re-renders
* UI updates

---

# 4. Key Differences Between State and Props

| Feature           | Props                     | State                    |
| ----------------- | ------------------------- | ------------------------ |
| Ownership         | Passed from parent        | Owned by component       |
| Mutable?          | No (Read-only)            | Yes                      |
| Controlled by     | Parent                    | Component itself         |
| Causes re-render? | Yes (when parent updates) | Yes (when state updates) |
| Used for          | Passing data              | Managing dynamic data    |

---

# 5. Real-World Example

Imagine an e-commerce app:

* Parent component fetches product details.
* Product details passed as props to ProductCard component.
* ProductCard has state for "isAddedToCart".

Props = Product information
State = Whether user clicked "Add to Cart"

---

# 6. Combined Example (State + Props Together)

```jsx
function Parent() {
  const [name, setName] = useState('Saurabh');

  return (
    <div>
      <Child name={name} />
      <button onClick={() => setName('Rahul')}>
        Change Name
      </button>
    </div>
  );
}

function Child({ name }) {
  return <h1>Hello {name}</h1>;
}
```

Here:

* name is state in Parent.
* Passed as props to Child.
* When state changes, Child re-renders.

---

# 7. Common Mistakes

❌ Modifying props directly

```jsx
props.name = 'New Name';  // Wrong
```

❌ Treating state as normal variable

```jsx
count = count + 1; // Wrong
```

Correct way:

```jsx
setCount(count + 1);
```

---

# 8. Interview Questions & Answers

### Q1: What is the difference between state and props?

Answer:
Props are read-only data passed from parent to child. State is internal data managed by the component itself.

---

### Q2: Can a component modify its props?

Answer:
No. Props are immutable.

---

### Q3: When does a component re-render?

Answer:
When state changes or when props change.

---

### Q4: Is state private to a component?

Answer:
Yes. State belongs only to the component that defines it.

---

### Q5: How do props flow in React?

Answer:
Props flow in one direction — from parent to child (unidirectional data flow).

---

# 9. Advanced Interview Insight

Interviewers often ask:

"If child needs to update parent state, what will you do?"

Answer:
Pass a function from parent to child as props.

Example:

```jsx
function Parent() {
  const [count, setCount] = useState(0);

  return <Child increment={() => setCount(count + 1)} />;
}

function Child({ increment }) {
  return <button onClick={increment}>Increase</button>;
}
```

---

# 10. Key Takeaways

* Props = external data (read-only).
* State = internal data (changeable).
* React follows unidirectional data flow.
* State updates trigger re-render.
* Props help build reusable components.

---

If preparing for interviews, make sure you can:

* Clearly explain unidirectional data flow
* Explain re-render behavior
* Give parent-child example
* Explain why props are immutable

This is a very fundamental React question and almost always asked in interviews.
