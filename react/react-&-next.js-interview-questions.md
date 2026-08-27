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

```text
useMemo     → Memoizes a value
useCallback → Memoizes a function
```

Do not use them everywhere. Memoization also has a cost.

---

# 14. What happens when you fetch data directly inside a Server Component in Next.js?

Example:

```jsx
export default async function Page() {
  const response = await fetch("https://api.example.com/products");

  const products = await response.json();

  return <ProductList products={products} />;
}
```

The fetch runs on the server.

Benefits:

* No client-side loading JavaScript required for that fetch.
* Secrets can remain on the server.
* Database or backend access can stay private.
* Server rendering can include the fetched data.

The client receives the rendered result and the required React payload.

---

# 15. How does Next.js cache server data?

Next.js provides several caching mechanisms depending on the API and rendering setup.

For `fetch`, you can control revalidation:

```js
fetch("https://api.example.com/data", {
  next: {
    revalidate: 60
  }
});
```

You can also opt out of persistent caching:

```js
fetch("https://api.example.com/data", {
  cache: "no-store"
});
```

Common caching concepts include:

* Request memoization
* Data caching
* Full route caching
* Router/client cache
* Time-based revalidation
* On-demand revalidation

The exact behavior can depend on the Next.js version and rendering configuration.

---

# 16. How do you optimize a heavy chart in Next.js?

Strategies:

## Dynamically import the chart

```jsx
import dynamic from "next/dynamic";

const Chart = dynamic(() => import("./Chart"), {
  ssr: false,
});
```

## Reduce data points

Instead of rendering millions of points:

* Aggregate data
* Downsample data
* Paginate
* Load ranges dynamically

## Memoize expensive calculations

```jsx
const chartData = useMemo(() => {
  return processData(data);
}, [data]);
```

## Move expensive calculations

Process large datasets:

* On the server
* In a Web Worker
* Before passing data to the chart

## Virtualize related UI

Avoid rendering unnecessary surrounding elements.

---

# 17. How do you optimize the same API call in Next.js?

If multiple Server Components request the same data, you should avoid unnecessary duplicate work.

Create a shared data function:

```js
export async function getUser(id) {
  const response = await fetch(
    `https://api.example.com/users/${id}`
  );

  return response.json();
}
```

Then reuse it.

For non-`fetch` data sources such as database calls, React's `cache()` can be useful:

```js
import { cache } from "react";

export const getUser = cache(async (id) => {
  return db.user.findUnique({
    where: { id }
  });
});
```

Also use appropriate:

* Data caching
* Revalidation
* Request memoization
* Cache tags where appropriate

---

# 18. React lifecycle phases

React lifecycle can be understood in three major phases:

## Mounting

The component is added to the UI.

Functional equivalent:

```jsx
useEffect(() => {
  console.log("Mounted");
}, []);
```

## Updating

The component re-renders because of:

* State changes
* Props changes
* Context changes

```jsx
useEffect(() => {
  console.log("Updated");
}, [value]);
```

## Unmounting

The component is removed.

```jsx
useEffect(() => {
  return () => {
    console.log("Cleanup");
  };
}, []);
```

For class components, common lifecycle methods include:

* `componentDidMount`
* `componentDidUpdate`
* `componentWillUnmount`

---

# 19. How does nested routing work in Next.js?

With the App Router:

```text
app/
├── dashboard/
│   ├── layout.js
│   ├── page.js
│   └── settings/
│       └── page.js
```

Routes:

```text
/dashboard
/dashboard/settings
```

The `layout.js` can wrap nested pages.

Example:

```jsx
export default function DashboardLayout({ children }) {
  return (
    <>
      <Sidebar />
      {children}
    </>
  );
}
```

Nested pages inherit layouts from parent route segments.

---

# 20. What are Server Components and Client Components?

## Server Component

Runs on the server.

Benefits:

* Can access server resources.
* Can fetch data directly.
* Can keep secrets on the server.
* Does not automatically add its component code to the client bundle.

Example:

```jsx
export default async function Page() {
  const users = await getUsers();

  return <UserList users={users} />;
}
```

## Client Component

Uses:

```jsx
"use client";
```

Required for:

* `useState`
* `useEffect`
* Event handlers
* Browser APIs

Example:

```jsx
"use client";

import { useState } from "react";

export default function Counter() {
  const [count, setCount] = useState(0);

  return (
    <button onClick={() => setCount(count + 1)}>
      {count}
    </button>
  );
}
```

Best practice: Keep Client Components as small as possible.

---

# 21. How does dynamic routing work in Next.js?

Create a folder using square brackets:

```text
app/
└── blog/
    └── [slug]/
        └── page.js
```

URL:

```text
/blog/react-hooks
```

The route parameter is:

```text
slug = "react-hooks"
```

Example:

```jsx
export default async function Page({ params }) {
  const { slug } = await params;

  return <h1>{slug}</h1>;
}
```

You can also use:

```text
[...slug]      → Catch-all route
[[...slug]]    → Optional catch-all route
```

---

# 22. Tell me about Route Groups

Route groups use parentheses:

```text
app/
├── (marketing)/
│   └── about/
│       └── page.js
│
└── (dashboard)/
    └── profile/
        └── page.js
```

The group name does not appear in the URL.

URLs:

```text
/about
/profile
```

Route groups help organize:

* Authentication routes
* Marketing pages
* Dashboard pages
* Different layouts

---

# 23. How do we maintain a protected route?

You can protect routes at different levels.

## Middleware / Proxy

Check authentication before allowing access to routes.

## Server Component

Verify the user on the server:

```jsx
export default async function Dashboard() {
  const user = await getCurrentUser();

  if (!user) {
    redirect("/login");
  }

  return <DashboardUI />;
}
```

## Client-side protection

Useful for UI behavior, but it should not be the only security layer.

Important: Real authorization should be validated on the server.

---

# 24. Nested route is not working. How do you find and fix the issue?

Check:

### 1. Folder structure

```text
app/dashboard/settings/page.js
```

### 2. Missing `page.js`

A route requires a `page.js`, `page.jsx`, `page.ts`, or `page.tsx`.

### 3. Incorrect navigation

```jsx
<Link href="/dashboard/settings">
  Settings
</Link>
```

### 4. Route conflicts

Check:

* Dynamic routes
* Catch-all routes
* Route groups

### 5. Layout issues

Check whether the layout correctly renders:

```jsx
{children}
```

### 6. Middleware or Proxy

Authentication logic may redirect the request.

### 7. Check terminal and browser errors

Use the Next.js error output to identify:

* Import errors
* Rendering errors
* Route conflicts

---

# 25. How do we set client-side and server-side cookies?

## Client-side cookies

For non-sensitive cookies, browser-side libraries can be used.

However, sensitive authentication tokens should generally not be accessible to client JavaScript.

## Server-side cookies

In the App Router, use the server-side cookies API:

```js
import { cookies } from "next/headers";

const cookieStore = await cookies();

const token = cookieStore.get("token");
```

For authentication, prefer secure cookies with appropriate flags such as:

* `httpOnly`
* `secure`
* `sameSite`

Avoid storing sensitive authentication tokens in places easily accessible to JavaScript when an `HttpOnly` cookie architecture is appropriate.

---

# 26. How do you securely handle form user input?

Important steps:

### Validate input

Use schema validation:

```js
const schema = z.object({
  email: z.string().email(),
  password: z.string().min(8),
});
```

### Sanitize when appropriate

Protect against malicious input depending on how the data will be used.

### Never trust client-side validation

Always validate again on the server.

### Prevent injection attacks

Use:

* Parameterized database queries
* ORM protections
* Proper escaping

### Add authentication and authorization

Verify that the user has permission to perform the action.

### Protect sensitive actions

Consider:

* CSRF protections where relevant
* Rate limiting
* Secure cookies
* Content Security Policy

---

# 27. How does the `useEffect` dependency array work internally?

Conceptually, React stores information about the previous dependencies.

Example:

```jsx
useEffect(() => {
  fetchUser(userId);
}, [userId]);
```

During a new render, React compares the current dependency values with the previous dependency values.

Conceptually:

```text
Previous: [1]
Current:  [2]

Changed → Run cleanup → Run effect
```

React uses `Object.is()` semantics for dependency comparison.

Important issue:

```jsx
useEffect(() => {
  // ...
}, [{}]);
```

A new object is created every render, so the dependency changes every time.

---

# 28. What is Middleware / `proxy.ts` in Next.js?

In newer Next.js versions, `proxy.ts` is the convention replacing the older `middleware.ts` naming.

It can run before requests reach routes and can be used for:

* Authentication checks
* Redirects
* Request rewriting
* Header modification
* Basic request filtering

Example concept:

```ts
export function proxy(request: Request) {
  // Check request
}
```

Use route matching carefully so unnecessary routes are not processed.

For complex authentication and authorization, keep security logic maintainable and validate access close to sensitive server resources as well.

---

# 29. How do we handle authentication in Server Components?

A Server Component can read the user's session or secure cookie on the server.

Example flow:

```text
Request
   ↓
Read session/cookie
   ↓
Validate user
   ↓
Authorized? ── No → Redirect/Login
   ↓ Yes
Render protected data
```

Example:

```jsx
export default async function Dashboard() {
  const user = await getCurrentUser();

  if (!user) {
    redirect("/login");
  }

  return <h1>Welcome {user.name}</h1>;
}
```

Authorization should also be checked when accessing sensitive data or performing mutations.

---

# 30. How do you structure a large-scale React/Next.js project?

A good approach is feature-based organization.

Example:

```text
src/
├── app/
│   ├── (marketing)/
│   ├── (dashboard)/
│   └── api/
│
├── components/
│   ├── ui/
│   └── shared/
│
├── features/
│   ├── auth/
│   │   ├── components/
│   │   ├── services/
│   │   ├── hooks/
│   │   └── types/
│   │
│   └── products/
│
├── lib/
│   ├── db/
│   ├── auth/
│   └── utils/
│
├── hooks/
├── types/
└── config/
```

Principles:

* Group related code by feature.
* Separate reusable UI from business logic.
* Keep server-only code separate.
* Use consistent naming.
* Avoid deeply nested unrelated folders.
* Define clear API and data boundaries.

