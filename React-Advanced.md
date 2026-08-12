# ⚛️ 04 — React Advanced Topics: Routing, Performance & Patterns

## 📖 Topics Covered

* `useReducer`
* `useMemo`
* `useCallback`
* React Router
* Client-side Routing
* `useNavigate`
* `Link`
* Custom Hooks
* Lazy Loading
* Error Boundaries
* Context API vs Redux
* Reconciliation
* `React.Fragment`
* Form Handling
* `react-hook-form`
* Code Splitting
* Portals
* Functional Component Lifecycle

> **Note:** The uploaded React Fundamentals material covers Q31–Q45 and provides related background such as Hooks, Context API, `React.memo`, re-rendering, and common advanced interview topics. The questions below (Q46–Q60) were not directly answered in the uploaded source, so these answers extend the material using standard React concepts. fileciteturn0file0

---

## Q46. What is the `useReducer` Hook and when is it preferred over `useState`?

**Answer:**

`useReducer` is a React Hook used to manage **complex state logic** in functional components.

It works with:

* **State** → current state
* **Action** → describes what happened
* **Reducer** → function that calculates the next state
* **dispatch** → sends an action to the reducer

**Example:**

```jsx
import { useReducer } from "react";

const initialState = { count: 0 };

function reducer(state, action) {
  switch (action.type) {
    case "increment":
      return { count: state.count + 1 };

    case "decrement":
      return { count: state.count - 1 };

    default:
      return state;
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, initialState);

  return (
    <div>
      <p>Count: {state.count}</p>

      <button onClick={() => dispatch({ type: "increment" })}>
        Increment
      </button>

      <button onClick={() => dispatch({ type: "decrement" })}>
        Decrement
      </button>
    </div>
  );
}
```

### When should you prefer `useReducer`?

Use `useReducer` when:

* State logic is complex.
* Multiple state values are related.
* Many different actions can update the state.
* State transitions need to be predictable and centralized.
* You want reducer logic that is easier to test.

For simple state such as a boolean, string, or counter, `useState` is usually simpler.

---

## Q47. Explain the `useMemo` Hook and give a use case.

**Answer:**

`useMemo` is a React Hook used to **memoize the result of an expensive calculation**.

React stores the calculated value and recomputes it only when one of its dependencies changes.

**Example:**

```jsx
import { useMemo } from "react";

function ProductList({ products, search }) {
  const filteredProducts = useMemo(() => {
    return products.filter((product) =>
      product.name.toLowerCase().includes(search.toLowerCase())
    );
  }, [products, search]);

  return (
    <ul>
      {filteredProducts.map((product) => (
        <li key={product.id}>{product.name}</li>
      ))}
    </ul>
  );
}
```

Here, `filteredProducts` is recalculated only when `products` or `search` changes.

### When should you use it?

Use `useMemo` when:

* A calculation is expensive.
* The calculation happens frequently.
* The dependencies do not change often.
* Profiling shows that memoization improves performance.

**Important:** Do not use `useMemo` for every calculation. It is a performance optimization and can add unnecessary complexity.

---

## Q48. What is the `useCallback` Hook and when do you use it?

**Answer:**

`useCallback` is a React Hook that **memoizes a function reference**.

It returns the same function reference between renders until one of its dependencies changes.

**Example:**

```jsx
import { useCallback, useState } from "react";

function App() {
  const [count, setCount] = useState(0);

  const handleClick = useCallback(() => {
    console.log("Button clicked");
  }, []);

  return (
    <div>
      <p>{count}</p>

      <button onClick={() => setCount(count + 1)}>
        Increment
      </button>

      <button onClick={handleClick}>
        Click
      </button>
    </div>
  );
}
```

### Common use case

`useCallback` is especially useful when passing a callback to a component optimized with `React.memo`.

```jsx
const User = React.memo(function User({ onSelect }) {
  return <button onClick={onSelect}>Select User</button>;
});
```

If the parent creates a new function on every render, the child may re-render because the function prop has a new reference. `useCallback` can help keep the function reference stable.

**Important:** `useCallback` should be used when function identity matters for optimization. It should not be added to every function automatically.

---

## Q49. What is React Router and how do you set up client-side routing?

**Answer:**

**React Router** is a routing library used to manage navigation between different views or pages in a React application without performing a full browser page reload.

### Basic setup

Install React Router:

```bash
npm install react-router-dom
```

Then define routes:

```jsx
import { BrowserRouter, Routes, Route } from "react-router-dom";

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
        <Route path="/contact" element={<Contact />} />
      </Routes>
    </BrowserRouter>
  );
}
```

Here:

* `BrowserRouter` provides routing functionality.
* `Routes` contains the application's routes.
* `Route` maps a URL path to a React component.

### Navigation

```jsx
import { Link } from "react-router-dom";

<Link to="/about">About</Link>
```

Clicking the link changes the route without performing a traditional full-page reload.

---

## Q50. What is the difference between `useNavigate` and `Link` in React Router?

**Answer:**

Both are used for navigation, but they are intended for different situations.

### `Link`

`Link` is used for **declarative navigation**.

```jsx
import { Link } from "react-router-dom";

<Link to="/dashboard">
  Dashboard
</Link>
```

It is commonly used in:

* Navigation bars
* Menus
* Buttons that act as normal links
* User-facing navigation

### `useNavigate`

`useNavigate` is used for **programmatic navigation**.

```jsx
import { useNavigate } from "react-router-dom";

function Login() {
  const navigate = useNavigate();

  const handleLogin = () => {
    // After successful login
    navigate("/dashboard");
  };

  return <button onClick={handleLogin}>Login</button>;
}
```

### Difference

| `Link` | `useNavigate` |
|---|---|
| Declarative navigation | Programmatic navigation |
| Used directly in JSX | Used inside component logic |
| Good for menus and links | Good after actions/events |
| Uses `to` prop | Uses `navigate()` |

---

## Q51. What are custom Hooks in React? Write a simple example.

**Answer:**

Custom Hooks are **reusable JavaScript functions that use React Hooks** to share stateful logic between components.

A custom Hook name should normally start with `use`.

### Example

```jsx
import { useEffect, useState } from "react";

function useWindowWidth() {
  const [width, setWidth] = useState(window.innerWidth);

  useEffect(() => {
    const handleResize = () => {
      setWidth(window.innerWidth);
    };

    window.addEventListener("resize", handleResize);

    return () => {
      window.removeEventListener("resize", handleResize);
    };
  }, []);

  return width;
}
```

Now a component can use it:

```jsx
function App() {
  const width = useWindowWidth();

  return <h1>Window width: {width}px</h1>;
}
```

### Benefits

* Reuse logic between components
* Keep components cleaner
* Reduce duplicate code
* Make complex logic easier to organize and test

---

## Q52. What is lazy loading in React and how is it implemented?

**Answer:**

Lazy loading means **loading a component only when it is needed** instead of loading it immediately with the initial application bundle.

React provides `lazy()` and `Suspense` for this.

**Example:**

```jsx
import { lazy, Suspense } from "react";

const About = lazy(() => import("./About"));

function App() {
  return (
    <Suspense fallback={<p>Loading...</p>}>
      <About />
    </Suspense>
  );
}
```

Here:

* `lazy()` dynamically loads the component.
* `Suspense` displays fallback UI while the component is loading.

### Benefits

* Smaller initial JavaScript bundle
* Faster initial page loading
* Better performance for large applications

Lazy loading is commonly used for route-level components.

---

## Q53. What are React Error Boundaries and why are they useful?

**Answer:**

Error Boundaries are React components that **catch JavaScript errors in their child component tree** during rendering and certain lifecycle operations, then display fallback UI instead of allowing the entire UI to fail.

Traditionally, Error Boundaries are implemented using a **class component**.

**Example:**

```jsx
import React from "react";

class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);

    this.state = {
      hasError: false,
    };
  }

  static getDerivedStateFromError() {
    return {
      hasError: true,
    };
  }

  componentDidCatch(error, errorInfo) {
    console.error(error, errorInfo);
  }

  render() {
    if (this.state.hasError) {
      return <h2>Something went wrong.</h2>;
    }

    return this.props.children;
  }
}
```

Usage:

```jsx
<ErrorBoundary>
  <Dashboard />
</ErrorBoundary>
```

### Why are Error Boundaries useful?

They can:

* Prevent a rendering error from breaking the entire UI.
* Display a user-friendly fallback.
* Help developers log errors.
* Isolate failures to specific parts of an application.

**Important:** Error Boundaries do not catch every type of error, such as most event-handler errors or errors in asynchronous callbacks.

---

## Q54. What is the Context API and when should you use Redux instead?

**Answer:**

The **Context API** allows data to be shared between components without manually passing props through every level.

It is useful for relatively stable or broadly needed values such as:

* Theme
* Current user
* Language
* Application settings

**Example:**

```jsx
import { createContext, useContext } from "react";

const ThemeContext = createContext("light");

function Button() {
  const theme = useContext(ThemeContext);

  return <button className={theme}>Click</button>;
}

function App() {
  return (
    <ThemeContext.Provider value="dark">
      <Button />
    </ThemeContext.Provider>
  );
}
```

### When should you use Redux?

Redux is useful when an application has:

* Complex global state.
* Many components reading and updating shared state.
* Complicated state transitions.
* A need for centralized state management.
* A need for predictable update patterns and strong debugging/developer tooling.

### Context API vs Redux

| Context API | Redux |
|---|---|
| Built into React | External state-management library |
| Simple to set up | More structured |
| Good for shared/stable values | Good for complex global state |
| Less boilerplate for simple cases | Useful for larger state-management needs |
| Not a complete state-management solution by itself | Provides a full state-management pattern |

**Rule of thumb:** Use Context when it solves the problem simply. Consider Redux when global state becomes large, complex, or difficult to manage with local state and Context alone.

---

## Q55. Explain the concept of reconciliation in React.

**Answer:**

**Reconciliation** is the process React uses to determine what needs to change in the UI when state or props change.

When a component updates, React creates a new element tree and compares it with the previous tree.

A simplified process is:

1. State or props change.
2. React re-renders the relevant component.
3. React creates a new element tree.
4. React compares the new tree with the previous one.
5. React determines the necessary DOM updates.
6. The browser DOM is updated accordingly.

React uses concepts such as **element type and keys** to determine whether existing elements can be reused or need to be replaced.

For lists, stable keys are particularly important because they help React correctly identify items.

---

## Q56. What is the difference between `React.Fragment` and empty tags (`<>`)?

**Answer:**

Both `React.Fragment` and the shorthand syntax `<>...</>` allow you to group multiple elements **without adding an extra DOM element**.

### `React.Fragment`

```jsx
import React from "react";

function App() {
  return (
    <React.Fragment>
      <h1>Hello</h1>
      <p>Welcome</p>
    </React.Fragment>
  );
}
```

### Fragment shorthand

```jsx
function App() {
  return (
    <>
      <h1>Hello</h1>
      <p>Welcome</p>
    </>
  );
}
```

### Main difference

The shorthand syntax is shorter, but it **cannot receive props**, including a `key`.

For example, when rendering a list of multiple elements, use:

```jsx
items.map((item) => (
  <React.Fragment key={item.id}>
    <h2>{item.title}</h2>
    <p>{item.description}</p>
  </React.Fragment>
));
```

---

## Q57. How do you handle forms in React? Explain with Formik or `react-hook-form`.

**Answer:**

Forms in React can be handled using controlled inputs, uncontrolled inputs, or form libraries such as **Formik** and **react-hook-form**.

`react-hook-form` is popular because it provides form state management and validation while minimizing unnecessary re-renders.

### Example with `react-hook-form`

Install it:

```bash
npm install react-hook-form
```

Then:

```jsx
import { useForm } from "react-hook-form";

function LoginForm() {
  const {
    register,
    handleSubmit,
    formState: { errors },
  } = useForm();

  const onSubmit = (data) => {
    console.log(data);
  };

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <input
        {...register("email", {
          required: "Email is required",
        })}
        type="email"
        placeholder="Email"
      />

      {errors.email && <p>{errors.email.message}</p>}

      <input
        {...register("password", {
          required: "Password is required",
          minLength: {
            value: 6,
            message: "Password must be at least 6 characters",
          },
        })}
        type="password"
        placeholder="Password"
      />

      {errors.password && <p>{errors.password.message}</p>}

      <button type="submit">Login</button>
    </form>
  );
}
```

### Important `react-hook-form` features

* `register()` → registers inputs.
* `handleSubmit()` → handles form submission.
* `formState.errors` → provides validation errors.
* Validation rules can be defined directly with `register()`.

For larger forms, it can also be combined with schema validation libraries such as **Zod**.

---

## Q58. What is code splitting in React and how does it improve performance?

**Answer:**

**Code splitting** means dividing the application's JavaScript bundle into smaller chunks that can be loaded when they are needed.

Without code splitting, a large application may send a large JavaScript bundle to the browser during the initial load.

With code splitting, only the code needed initially is loaded, while other parts can be loaded later.

### Example

```jsx
import { lazy } from "react";

const Dashboard = lazy(() => import("./Dashboard"));
```

This creates a separate chunk for the `Dashboard` component that can be loaded when required.

### Benefits

* Smaller initial bundle
* Faster initial loading
* Less JavaScript downloaded at startup
* Better performance for large applications

### Common ways to implement it

* `React.lazy()`
* Dynamic `import()`
* Route-level lazy loading

Code splitting and lazy loading are closely related: code splitting creates separate chunks, while lazy loading determines when some of those chunks are loaded.

---

## Q59. What are Portals in React and when are they useful?

**Answer:**

React Portals allow you to **render a component into a different DOM node outside its normal parent DOM hierarchy**.

Portals are useful when a UI element needs to visually escape its parent's DOM structure.

Common use cases include:

* Modals
* Dialogs
* Tooltips
* Dropdowns
* Toast notifications

### Example

HTML:

```html
<div id="root"></div>
<div id="modal-root"></div>
```

React:

```jsx
import { createPortal } from "react-dom";

function Modal({ children }) {
  const modalRoot = document.getElementById("modal-root");

  return createPortal(
    <div className="modal">
      {children}
    </div>,
    modalRoot
  );
}
```

Usage:

```jsx
function App() {
  return (
    <div>
      <h1>Main App</h1>

      <Modal>
        <h2>Hello from Modal</h2>
      </Modal>
    </div>
  );
}
```

The modal is rendered into `#modal-root` in the DOM, even though it is still part of the same React component tree.

---

## Q60. Explain the lifecycle of a React functional component with Hooks.

**Answer:**

A functional component does not use the old class lifecycle methods directly. Instead, its lifecycle behavior is handled through **rendering and Hooks such as `useEffect`**.

A simplified lifecycle can be understood in three stages:

### 1. Mounting

The component is rendered for the first time.

```jsx
function App() {
  useEffect(() => {
    console.log("Component mounted");
  }, []);

  return <h1>Hello</h1>;
}
```

With an empty dependency array, the effect runs after the initial render.

### 2. Updating

The component re-renders when its **state or props change**.

```jsx
const [count, setCount] = useState(0);

useEffect(() => {
  console.log("Count changed:", count);
}, [count]);
```

This effect runs after renders where `count` has changed.

### 3. Unmounting

The component is removed from the UI.

An effect can return a cleanup function:

```jsx
useEffect(() => {
  const handleResize = () => {
    console.log(window.innerWidth);
  };

  window.addEventListener("resize", handleResize);

  return () => {
    window.removeEventListener("resize", handleResize);
  };
}, []);
```

The cleanup function runs when the component unmounts.

### Simplified lifecycle

```text
Mount
  ↓
Render
  ↓
Effects run
  ↓
State/Props change
  ↓
Re-render
  ↓
Previous effect cleanup
  ↓
New effect runs
  ↓
Unmount
  ↓
Final cleanup
```

### Important point

The exact timing of effects depends on the Hook and React's rendering behavior. `useEffect` runs after the component is committed to the DOM, while `useLayoutEffect` runs synchronously after DOM mutations and before the browser paints.

---

# 💼 Common React Advanced Interview Follow-up Questions

These questions are commonly asked after Q46–Q60:

* What is the difference between `useMemo` and `useCallback`?
* When should you avoid `useMemo`?
* When should you avoid `useCallback`?
* What is the difference between `useState` and `useReducer`?
* What is the difference between lazy loading and code splitting?
* What is `Suspense` in React?
* What is the difference between `Link` and an HTML `<a>` tag?
* What is nested routing in React Router?
* What are route parameters?
* What is programmatic navigation?
* What is the difference between Context API and Redux?
* What is reconciliation?
* Why are keys important during reconciliation?
* What is an Error Boundary?
* Can functional components directly act as Error Boundaries?
* What is a React Portal?
* Why are Portals useful for modals?
* What is a custom Hook?
* What is the difference between controlled and uncontrolled forms?
* Why is `react-hook-form` useful?
* What is the difference between `React.lazy()` and dynamic `import()`?
* How can you improve React application performance?
