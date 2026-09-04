# ⚛️ 03 — React Fundamentals

## 📖 Topics Covered

* React Fundamentals
* Components
* JSX
* Virtual DOM
* Props
* State
* Hooks
* `useState`
* `useEffect`
* `useContext`
* `useRef`
* Controlled & Uncontrolled Components
* Prop Drilling
* Conditional Rendering
* React Keys
* `React.memo`

---

## Q31. What is React and what problem does it solve?

**Answer:**

React is a **JavaScript library for building user interfaces**, especially single-page applications.

It helps developers build complex and interactive UIs using **reusable components** and efficiently update the UI when data changes.

**Key benefits:**

* Component-based architecture
* Reusable UI components
* Efficient UI updates
* Declarative programming
* Large ecosystem

---

## Q32. What is JSX and why is it used in React?

**Answer:**

JSX stands for **JavaScript XML**. It allows us to write HTML-like syntax inside JavaScript.

JSX makes React code easier to read and helps developers describe what the UI should look like.

**Example:**

```jsx
const element = <h1>Hello, Shohag!</h1>;
```

JSX is converted into JavaScript before it runs in the browser.

---

## Q33. What is the difference between functional and class components?

**Answer:**

### Functional Component

A functional component is a JavaScript function that returns JSX.

```jsx
function Welcome() {
  return <h1>Hello World</h1>;
}
```

### Class Component

A class component is a JavaScript class that extends `React.Component`.

```jsx
class Welcome extends React.Component {
  render() {
    return <h1>Hello World</h1>;
  }
}
```

### Main Differences

| Functional Component      | Class Component        |
| ------------------------- | ---------------------- |
| JavaScript function       | JavaScript class       |
| Uses Hooks                | Uses lifecycle methods |
| Less code                 | More boilerplate       |
| Preferred in modern React | Mostly legacy code     |

Modern React generally prefers **functional components with Hooks**.

---

## Q34. What is the Virtual DOM and how does React use it?

**Answer:**

The Virtual DOM is a **lightweight JavaScript representation of the real DOM**.

When state or props change, React:

1. Creates a new Virtual DOM representation.
2. Compares it with the previous one.
3. Identifies what changed.
4. Updates only the necessary parts of the real DOM.

This process helps React update the UI efficiently.

---

## Q35. Explain the `useState` Hook with an example.

**Answer:**

`useState` is a React Hook used to add and manage **state in functional components**.

**Example:**

```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>

      <button onClick={() => setCount(count + 1)}>
        Increment
      </button>
    </div>
  );
}
```

Here:

* `count` → current state
* `setCount` → function used to update the state
* `0` → initial value

When `setCount()` updates the state, React re-renders the component.

---

## Q36. What is the `useEffect` Hook and what are its use cases?

**Answer:**

`useEffect` is a React Hook used to perform **side effects** in a functional component.

Common use cases include:

* Fetching data from an API
* Setting up event listeners
* Updating the document title
* Working with timers
* Subscribing to external services
* Cleaning up resources

**Example:**

```jsx
import { useEffect } from "react";

useEffect(() => {
  console.log("Component mounted");
}, []);
```

The empty dependency array means the effect runs after the initial render.

---

## Q37. What is the difference between controlled and uncontrolled components?

**Answer:**

### Controlled Component

In a controlled component, the form input value is controlled by **React state**.

```jsx
const [name, setName] = useState("");

<input
  value={name}
  onChange={(e) => setName(e.target.value)}
/>
```

### Uncontrolled Component

In an uncontrolled component, the input value is managed by the **DOM itself**, usually accessed using `useRef`.

```jsx
const inputRef = useRef();

<input ref={inputRef} />
```

### Difference

| Controlled            | Uncontrolled            |
| --------------------- | ----------------------- |
| Uses React state      | Uses DOM state          |
| More control          | Less React code         |
| Easier validation     | Useful for simple forms |
| Common in React forms | Uses `useRef`           |

---

## Q38. What are props in React and how are they passed?

**Answer:**

Props, short for **properties**, are used to pass data from a parent component to a child component.

Props are **read-only** and should not be modified by the child component.

**Example:**

```jsx
function User({ name }) {
  return <h2>Hello, {name}</h2>;
}

function App() {
  return <User name="Shohag" />;
}
```

Here, `name="Shohag"` is passed from `App` to `User` as a prop.

---

## Q39. What is prop drilling and how can it be avoided?

**Answer:**

**Prop drilling** happens when data needs to be passed through multiple components that do not actually need the data themselves.

For example:

```text
App
 ↓
Parent
 ↓
Child
 ↓
GrandChild
```

If `App` needs to pass data to `GrandChild`, it may have to pass the data through `Parent` and `Child`.

### How to avoid prop drilling:

* Context API
* `useContext`
* Redux
* Zustand
* Other state-management libraries

For smaller applications, **Context API** can be a simple solution.

---

## Q40. Explain the `useContext` Hook with an example.

**Answer:**

`useContext` allows a component to access data from a React Context without passing props manually through every component.

**Example:**

```jsx
import { createContext, useContext } from "react";

const UserContext = createContext();

function User() {
  const user = useContext(UserContext);

  return <h2>{user.name}</h2>;
}

function App() {
  return (
    <UserContext.Provider value={{ name: "Shohag" }}>
      <User />
    </UserContext.Provider>
  );
}
```

Here, `User` directly accesses the user data using `useContext`.

---

## Q41. What is the `useRef` Hook and when would you use it?

**Answer:**

`useRef` is a React Hook that allows us to store a value that persists between renders **without causing a re-render when the value changes**.

It is commonly used for:

* Accessing DOM elements
* Focusing an input
* Storing previous values
* Keeping mutable values between renders
* Working with timers

**Example:**

```jsx
import { useRef } from "react";

function Input() {
  const inputRef = useRef(null);

  const handleFocus = () => {
    inputRef.current.focus();
  };

  return (
    <>
      <input ref={inputRef} />

      <button onClick={handleFocus}>
        Focus Input
      </button>
    </>
  );
}
```

---

## Q42. What are React Keys and why are they important in lists?

**Answer:**

Keys are unique values that help React identify which items in a list have changed, been added, or removed.

**Example:**

```jsx
const users = [
  { id: 1, name: "Shohag" },
  { id: 2, name: "Hasan" }
];

users.map((user) => (
  <div key={user.id}>
    {user.name}
  </div>
));
```

Keys help React efficiently update lists.

**Best practice:** Use a **stable and unique ID** as the key instead of the array index whenever possible.

---

## Q43. What is the difference between state and props?

**Answer:**

| State                           | Props                              |
| ------------------------------- | ---------------------------------- |
| Managed by the component        | Passed from parent                 |
| Can be updated                  | Read-only                          |
| Used for internal data          | Used to pass data                  |
| Updating state causes re-render | Changing props can cause re-render |

**Example:**

```jsx
function User({ name }) {
  const [count, setCount] = useState(0);

  return (
    <div>
      <h2>{name}</h2>
      <p>{count}</p>
    </div>
  );
}
```

Here:

* `name` → prop
* `count` → state

---

## Q44. How does conditional rendering work in React?

**Answer:**

Conditional rendering means displaying different UI based on a condition.

React commonly uses:

* `if...else`
* Ternary operator
* Logical `&&`
* Logical `||`

### Ternary Example

```jsx
function App({ isLoggedIn }) {
  return (
    <div>
      {isLoggedIn ? (
        <h1>Welcome!</h1>
      ) : (
        <h1>Please Login</h1>
      )}
    </div>
  );
}
```

### Logical AND Example

```jsx
{isLoggedIn && <button>Logout</button>}
```

If `isLoggedIn` is `true`, the button is rendered.

---

## Q45. What is `React.memo` and when should you use it?

**Answer:**

`React.memo` is a performance optimization that prevents a functional component from re-rendering when its props have not changed.

**Example:**

```jsx
import React from "react";

const User = React.memo(function User({ name }) {
  console.log("User rendered");

  return <h2>{name}</h2>;
});
```

If the parent component re-renders but the `name` prop remains the same, React can skip re-rendering the `User` component.

### When should you use it?

Use `React.memo` when:

* A component renders frequently.
* Its rendering is relatively expensive.
* Its props often remain unchanged.
* Profiling shows unnecessary re-renders.

**Important:** `React.memo` should not be used everywhere. It is a performance optimization, not a default requirement.

---

# 💼 Common React Interview Follow-up Questions

These questions are commonly asked after React fundamentals:

* What is reconciliation in React?
* What is the difference between re-rendering and DOM updating?
* What is the difference between `useEffect` and `useLayoutEffect`?
* What is the dependency array in `useEffect`?
* What happens when the dependency array is empty?
* Why should we not mutate React state directly?
* What is state lifting?
* What is component composition?
* What is the difference between Context API and Redux?
* When should you use `useMemo`?
* When should you use `useCallback`?
* What is the difference between `useRef` and `useState`?
* Why should array indexes generally not be used as React keys?
* What causes a React component to re-render?
* What is reconciliation?
* What are custom Hooks?
* What are error boundaries?
* What is lazy loading in React?
* What is `React.lazy()`?
* What is `Suspense`?
* How can you optimize React application performance?
