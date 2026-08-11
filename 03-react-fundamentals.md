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



