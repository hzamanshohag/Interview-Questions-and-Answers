# React & Next.js Interview Questions and Answers

A practical interview preparation guide covering React fundamentals, performance optimization, rendering, caching, routing, authentication, and Next.js architecture.

---

# 1. How does React reconciliation decide when and what to render?

React reconciliation is the process React uses to compare the **previous Virtual DOM** with the **new Virtual DOM**.

When state or props change:

1. React creates a new Virtual DOM tree.
2. It compares the new tree with the previous tree.
3. React identifies what changed.
4. Only the necessary DOM updates are committed.

React mainly uses:

* **Element type** — If the type changes, React may replace the entire subtree.
* **Props** — React checks changed props.
* **Keys** — React uses keys to identify elements in lists.
* **Component state** — State updates trigger a new render.

Example:

```jsx
function App() {
  const [count, setCount] = useState(0);

  return <h1>{count}</h1>;
}
```

When `count` changes, React re-renders the component and reconciles the result with the previous UI.

---

# 2. State vs Props

| State                            | Props                                            |
| -------------------------------- | ------------------------------------------------ |
| Managed inside the component     | Passed from parent to child                      |
| Can change over time             | Read-only from the child component's perspective |
| Updated using a setter function  | Changed by the parent                            |
| Used for component-specific data | Used for communication and configuration         |

Example:

```jsx
function Parent() {
  return <Profile name="Shohag" />;
}

function Profile({ name }) {
  const [age, setAge] = useState(25);

  return <h1>{name} - {age}</h1>;
}
```

Here:

* `name` is a prop.
* `age` is state.

---

# 3. Controlled vs Uncontrolled Components

## Controlled Component

React controls the form input using state.

```jsx
function Form() {
  const [name, setName] = useState("");

  return (
    <input
      value={name}
      onChange={(e) => setName(e.target.value)}
    />
  );
}
```

Use controlled components when you need:

* Validation
* Real-time UI updates
* Conditional form behavior
* Centralized form state

## Uncontrolled Component

The DOM manages the input value.

```jsx
function Form() {
  const inputRef = useRef();

  const handleSubmit = () => {
    console.log(inputRef.current.value);
  };

  return <input ref={inputRef} />;
}
```

Use uncontrolled components for simpler forms or integration with non-React code.

---

# 4. How does the `useEffect` dependency array work?

```jsx
useEffect(() => {
  // Side effect
}, [dependency]);
```

### No dependency array

```jsx
useEffect(() => {
  console.log("Runs after every render");
});
```

### Empty dependency array

```jsx
useEffect(() => {
  console.log("Runs after initial mount");
}, []);
```

### Specific dependencies

```jsx
useEffect(() => {
  console.log("Runs when userId changes");
}, [userId]);
```

React compares dependencies with their previous values using `Object.is()`.

If a dependency changes, React schedules the effect again.

---

# 5. How do you optimize list rendering in React? How do we use keys in `map()`?

Example:

```jsx
users.map((user) => (
  <UserCard key={user.id} user={user} />
));
```

Keys help React identify which items:

* Were added
* Were removed
* Were updated
* Changed position

Best practice:

```jsx
key={user.id}
```

Avoid using array indexes when the list can be reordered:

```jsx
key={index}
```

Other optimization techniques:

* `React.memo`
* Virtualization
* Pagination
* Infinite scrolling
* Memoization
* Stable callbacks

For very large lists, use libraries such as virtualization solutions that only render visible items.

---

# 6. Tell me about React Fiber

React Fiber is React's rendering architecture.

It allows React to:

* Break rendering work into smaller units.
* Prioritize important updates.
* Pause and resume rendering work.
* Improve responsiveness.
* Support concurrent rendering features.

For example, typing into an input should generally feel responsive even if another part of the application is rendering a heavy UI.

Fiber helps React prioritize that work.

---

# 7. CSR, SSR, SSG, and ISR

## CSR — Client-Side Rendering

The browser downloads JavaScript and renders the page.

```text
Server → JavaScript → Browser renders UI
```

Best for:

* Highly interactive applications
* User dashboards
* Private authenticated UI

---

## SSR — Server-Side Rendering

The server renders HTML for every request.

```text
Request → Server renders → HTML sent to browser
```

Best for:

* Dynamic SEO pages
* Frequently changing public content
* Request-specific data

---

## SSG — Static Site Generation

Pages are generated ahead of time.

```text
Build time → Generate HTML → Serve static page
```

Best for:

* Blogs
* Documentation
* Marketing pages

---

## ISR — Incremental Static Regeneration

ISR allows static pages to be regenerated after a configured period.

```js
fetch("https://api.example.com/products", {
  next: {
    revalidate: 60
  }
});
```

The page can remain fast like a static page while data is refreshed periodically.

---

# 8. What is the best case to use ISR?

ISR is ideal when:

* Data changes occasionally.
* You need good SEO.
* Full SSR for every request is unnecessary.
* You want static performance with periodic updates.

Examples:

* E-commerce product pages
* Blogs
* News pages with periodic updates
* Documentation
* Company profiles

Example:

```js
fetch("https://api.example.com/products", {
  next: {
    revalidate: 3600
  }
});
```

This allows data to be revalidated approximately every hour.

---

# 9. A component renders small data but still loads slowly. Why?

The amount of displayed data may not be the problem.

Possible causes:

### Expensive parent rendering

A parent component may be rendering repeatedly.

### Expensive JavaScript

```jsx
const result = heavyCalculation();
```

This calculation runs during rendering.

### Large bundle size

The component may import a heavy library.

### Slow API

The displayed data may be small, but the API response could be slow.

### Waterfall requests

One request waits for another.

### Unnecessary re-renders

Props may be changing unnecessarily.

### Heavy child components

The parent may look simple but contain expensive children.

Use:

* React DevTools Profiler
* Browser Performance tools
* Network tab
* `console.count()`
* Bundle analysis

---

# 10. After submitting a form, it resets. How do you solve it?

The issue may happen because:

* The page reloads.
* The component is remounted.
* Form state is reset.
* A navigation occurs after submission.

Prevent default browser submission:

```jsx
const handleSubmit = (e) => {
  e.preventDefault();

  // Submit logic
};
```

```jsx
<form onSubmit={handleSubmit}>
```

If the component remounts, investigate:

* Changing `key`
* Route navigation
* Conditional rendering
* Parent component changes

---

# 11. How do you find a re-render issue in React and Next.js?

Use several techniques.

## React DevTools Profiler

Check:

* Which component re-rendered.
* How long rendering took.
* What caused the render.

## Add logging

```jsx
console.log("Component rendered");
```

Or:

```jsx
console.count("Component render");
```

## Check unstable props

This creates a new object on every render:

```jsx
<Component config={{ theme: "dark" }} />
```

This creates a new function on every render:

```jsx
<Component onClick={() => handleClick()} />
```

Use memoization when appropriate:

```jsx
const config = useMemo(() => ({
  theme: "dark"
}), []);
```

Also investigate:

* Context updates
* Parent re-renders
* State updates
* Changing object references

---

# 12. When should we lift state up, and when should we avoid it?

Lift state up when multiple components need to share the same source of truth.

Example:

```text
Parent
 ├── SearchInput
 └── SearchResults
```

The parent manages:

```jsx
const [search, setSearch] = useState("");
```

Then passes it to both children.

Avoid lifting state too high when:

* Only one component needs it.
* It causes unnecessary re-renders.
* State becomes difficult to manage.
* Components become tightly coupled.

Keep state as close as possible to where it is used.

---

# 13. Difference between `useMemo` and `useCallback`

## `useMemo`

Memoizes a computed value.

```jsx
const filteredUsers = useMemo(() => {
  return users.filter((user) => user.active);
}, [users]);
```

## `useCallback`

Memoizes a function reference.

```jsx
const handleClick = useCallback(() => {
  console.log("Clicked");
}, []);
```

Summary:

