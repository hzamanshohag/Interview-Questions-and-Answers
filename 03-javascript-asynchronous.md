# 📚 03 — JavaScript Asynchronous Programming

## 📖 Topics Covered
- Synchronous vs Asynchronous Code
- Call Stack, Event Loop, and Queues
- Callbacks and Callback Hell
- Promises
- `async` / `await`
- Error Handling in Async Code
- Promise Combinators (`all`, `allSettled`, `race`, `any`)
- Microtasks vs Macrotasks
- `setTimeout()` / `setInterval()`
- Fetch API and AJAX
- Async Iteration
- Debouncing and Throttling

---

## Q1. What is the difference between synchronous and asynchronous code?

**Answer:**
- **Synchronous** code runs line by line, in order — each operation blocks the next until it finishes.
- **Asynchronous** code allows long-running operations (network requests, timers, file reads) to run in the background without blocking the rest of the program.

| Feature | Synchronous | Asynchronous |
|---------|-------------|----------------|
| Execution | Blocking | Non-blocking |
| Order | Guaranteed, sequential | May complete out of order |
| Common Uses | Simple calculations, loops | API calls, timers, file I/O |
| Mechanism | Direct function calls | Callbacks, Promises, `async/await` |

```javascript
// Synchronous
console.log("1");
console.log("2");
console.log("3");
// Output: 1, 2, 3 (in order)

// Asynchronous
console.log("1");
setTimeout(() => console.log("2"), 1000);
console.log("3");
// Output: 1, 3, 2 (setTimeout doesn't block)
```

> **Interview Tip:** JavaScript is **single-threaded** — it can only do one thing at a time. Asynchronous behavior is handled by the browser/Node.js APIs and the **event loop**, not by multiple threads.

---

## Q2. What is the Call Stack?

**Answer:**
The call stack is a data structure that tracks function execution — it's LIFO (Last In, First Out). Whenever a function is called, it's pushed onto the stack; when it returns, it's popped off.

```javascript
function multiply(a, b) { return a * b; }
function square(n) { return multiply(n, n); }
function printSquare(n) { console.log(square(n)); }

printSquare(4);
// Call stack: printSquare → square → multiply → (all pop off as they return)
```

If the stack grows too large (e.g., infinite recursion), it throws a `"Maximum call stack size exceeded"` error.

---

## Q3. What is the Event Loop?

**Answer:**
The event loop is the mechanism that allows JavaScript's single thread to handle asynchronous operations. It continuously checks: *"Is the call stack empty? If so, take the next task from the queue and push it onto the stack."*

**Simplified flow:**
1. Run all synchronous code (call stack).
2. Once the stack is empty, process all **microtasks** (Promises, `queueMicrotask`).
3. Then process one **macrotask** (`setTimeout`, `setInterval`, I/O).
4. Repeat.

```javascript
console.log("1 - sync");

setTimeout(() => console.log("2 - macrotask"), 0);

Promise.resolve().then(() => console.log("3 - microtask"));

console.log("4 - sync");

// Output order: 1 - sync, 4 - sync, 3 - microtask, 2 - macrotask
```

> **Interview Tip:** Microtasks (Promises) always run **before** macrotasks (`setTimeout`), even if the timeout is `0ms`. This trips up a lot of candidates.

---

## Q4. What are Microtasks and Macrotasks?

**Answer:**

| Feature | Microtasks | Macrotasks |
|---------|------------|-------------|
| Examples | `Promise.then/catch/finally`, `queueMicrotask`, `MutationObserver` | `setTimeout`, `setInterval`, `setImmediate`, I/O, UI rendering |
| Priority | Higher — runs first | Lower — runs after all microtasks |
| Queue drained | Fully drained before next macrotask | One task per event loop cycle |

```javascript
setTimeout(() => console.log("macrotask"), 0);
Promise.resolve().then(() => console.log("microtask 1"));
Promise.resolve().then(() => console.log("microtask 2"));

// Output: microtask 1, microtask 2, macrotask
// ALL microtasks run before the next macrotask
```

---

## Q5. What is a callback function?

**Answer:**
A callback is a function passed as an argument to another function, to be executed later — often after an asynchronous operation completes.

```javascript
function fetchData(callback) {
  setTimeout(() => {
    callback("Data received");
  }, 1000);
}

fetchData((result) => {
  console.log(result); // "Data received" (after 1 second)
});
```

Callbacks aren't inherently asynchronous (e.g., `array.map(callback)` is synchronous) — but they're the foundation of async patterns before Promises existed.

---

## Q6. What is callback hell, and how do you avoid it?

**Answer:**
Callback hell (the "pyramid of doom") happens when multiple nested asynchronous callbacks make code hard to read and maintain.

```javascript
// ❌ Callback hell
getUser(1, (user) => {
  getPosts(user.id, (posts) => {
    getComments(posts[0].id, (comments) => {
      console.log(comments); // deeply nested, hard to follow
    });
  });
});
```

**Solutions:**
```javascript
// ✅ Promises (flatter chain)
getUser(1)
  .then(user => getPosts(user.id))
  .then(posts => getComments(posts[0].id))
  .then(comments => console.log(comments))
  .catch(err => console.error(err));

// ✅ async/await (most readable)
async function loadData() {
  try {
    const user = await getUser(1);
    const posts = await getPosts(user.id);
    const comments = await getComments(posts[0].id);
    console.log(comments);
  } catch (err) {
    console.error(err);
  }
}
```

---

## Q7. What is a Promise?

**Answer:**
A Promise is an object representing the eventual completion (or failure) of an asynchronous operation. It has three states:

| State | Meaning |
|-------|---------|
| `pending` | Initial state, operation not finished |
| `fulfilled` | Operation completed successfully |
| `rejected` | Operation failed |

```javascript
const promise = new Promise((resolve, reject) => {
  const success = true;
  setTimeout(() => {
    if (success) {
      resolve("Operation successful");
    } else {
      reject("Operation failed");
    }
  }, 1000);
});

promise
  .then(result => console.log(result))   // runs if resolved
  .catch(error => console.error(error))  // runs if rejected
  .finally(() => console.log("Done"));   // always runs
```

> **Interview Tip:** A Promise is **settled** once it's either fulfilled or rejected — it cannot change state afterward.

---

## Q8. What is `async`/`await`?

**Answer:**
`async`/`await` is syntactic sugar built on top of Promises, letting asynchronous code be written in a synchronous-looking style.

- An `async` function always returns a Promise.
- `await` pauses execution inside an `async` function until the Promise settles.

```javascript
function fetchUser() {
  return new Promise(resolve => setTimeout(() => resolve({ name: "Shohag" }), 1000));
}

async function getUser() {
  console.log("Fetching...");
  const user = await fetchUser(); // pauses here until resolved
  console.log(user); // { name: "Shohag" }
  return user;
}

getUser().then(u => console.log("Done:", u));
```

**Comparison:**

| Feature | Promises (`.then()`) | `async`/`await` |
|---------|------------------------|-------------------|
| Readability | Chained, can get nested | Linear, synchronous-looking |
| Error handling | `.catch()` | `try/catch` |
| Debugging | Harder (stack traces) | Easier |

---

## Q9. How do you handle errors in asynchronous code?

**Answer:**
```javascript
// With Promises
fetchData()
  .then(data => process(data))
  .catch(error => console.error("Error:", error));

// With async/await
async function run() {
  try {
    const data = await fetchData();
    process(data);
  } catch (error) {
    console.error("Error:", error);
  } finally {
    console.log("Cleanup runs regardless");
  }
}

// Handling unhandled promise rejections globally (Node.js / browser)
window.addEventListener("unhandledrejection", (event) => {
  console.error("Unhandled:", event.reason);
});
```

> **Interview Tip:** A `try/catch` around `await` only catches errors from that specific asynchronous call — synchronous errors elsewhere in the block are also caught, but errors from un-awaited Promises won't be.

---

## Q10. What are `Promise.all()`, `Promise.allSettled()`, `Promise.race()`, and `Promise.any()`?

**Answer:**

| Method | Behavior | Rejects When |
|--------|----------|----------------|
| `Promise.all()` | Waits for all to resolve, returns array of results | If **any** promise rejects (fails fast) |
| `Promise.allSettled()` | Waits for all to settle (resolved or rejected) | Never — always resolves with status of each |
| `Promise.race()` | Resolves/rejects as soon as the **first** promise settles | If the first settled promise rejects |
| `Promise.any()` | Resolves as soon as the **first** promise fulfills | Only if **all** promises reject |

```javascript
const p1 = Promise.resolve(1);
const p2 = new Promise((res) => setTimeout(() => res(2), 100));
const p3 = Promise.reject("Error!");

Promise.all([p1, p2]).then(console.log); // [1, 2]

Promise.allSettled([p1, p3]).then(console.log);
// [{status:"fulfilled", value:1}, {status:"rejected", reason:"Error!"}]

Promise.race([p1, p2]).then(console.log); // 1 (settles first)

Promise.any([p3, p2]).then(console.log); // 2 (first fulfilled, ignores p3's rejection)
```

---

## Q11. What is the difference between `setTimeout()` and `setInterval()`?

**Answer:**

| Feature | `setTimeout()` | `setInterval()` |
|---------|------------------|---------------------|
| Runs | Once, after a delay | Repeatedly, at fixed intervals |
| Stop with | `clearTimeout(id)` | `clearInterval(id)` |

```javascript
const timeoutId = setTimeout(() => console.log("Runs once after 2s"), 2000);
clearTimeout(timeoutId); // cancels it before it runs

let count = 0;
const intervalId = setInterval(() => {
  console.log("Runs every 1s", ++count);
  if (count === 3) clearInterval(intervalId); // stop after 3 runs
}, 1000);
```

> **Interview Tip:** `setTimeout(fn, 0)` doesn't run immediately — it still waits for the call stack to clear and any pending microtasks to finish first, since it's a macrotask.

---

## Q12. How do you make an HTTP request in JavaScript?

**Answer:**
```javascript
// Using fetch() with Promises
fetch("https://api.example.com/users")
  .then(response => {
    if (!response.ok) throw new Error(`HTTP error: ${response.status}`);
    return response.json();
  })
  .then(data => console.log(data))
  .catch(error => console.error("Fetch failed:", error));

// Using fetch() with async/await (preferred, cleaner)
async function getUsers() {
  try {
    const response = await fetch("https://api.example.com/users");
    if (!response.ok) throw new Error(`HTTP error: ${response.status}`);
    const data = await response.json();
    return data;
  } catch (error) {
    console.error("Fetch failed:", error);
  }
}
```

> **Interview Tip:** `fetch()` only rejects on network failure — a 404 or 500 response is still a "successful" fetch. Always check `response.ok` or `response.status` manually.

---

## Q13. How do you run multiple asynchronous operations in parallel vs sequentially?

**Answer:**
```javascript
// ❌ Sequential (slower - each await blocks the next)
async function sequential() {
  const a = await fetchA(); // waits
  const b = await fetchB(); // waits after a finishes
  return [a, b];
}

// ✅ Parallel (faster - both start at the same time)
async function parallel() {
  const [a, b] = await Promise.all([fetchA(), fetchB()]);
  return [a, b];
}
```

Use sequential execution only when one call **depends** on the result of a previous one; otherwise, run independent calls in parallel with `Promise.all()` for better performance.

---

## Q14. What is a race condition in asynchronous JavaScript?

**Answer:**
A race condition occurs when the outcome of async operations depends on unpredictable timing — e.g., a slower request resolving after a faster one, overwriting newer data with stale data.

```javascript
// ❌ Problem: if searchAPI("a") resolves AFTER searchAPI("ab"),
// stale results for "a" overwrite the newer results for "ab"
let latestQuery = "";

async function search(query) {
  latestQuery = query;
  const results = await searchAPI(query);

  // ✅ Fix: ignore stale responses
  if (query !== latestQuery) return;
  updateUI(results);
}
```

Other common fixes: using `AbortController` to cancel outdated requests, or request IDs/timestamps to discard stale responses.

```javascript
const controller = new AbortController();
fetch(url, { signal: controller.signal });
controller.abort(); // cancels the in-flight request
```

---

## Q15. What is `async` iteration (`for await...of`)?

**Answer:**
`for await...of` iterates over an **async iterable** (like an array of Promises or an async generator), awaiting each value in sequence.

```javascript
async function processInOrder() {
  const promises = [fetchA(), fetchB(), fetchC()];

  for await (const result of promises) {
    console.log(result); // logs each result as it resolves, in order
  }
}

// Async generator example
async function* fetchPages() {
  for (let page = 1; page <= 3; page++) {
    yield await fetchAPI(`/data?page=${page}`);
  }
}

async function run() {
  for await (const page of fetchPages()) {
    console.log(page);
  }
}
```

---

## Q16. What is debouncing?

**Answer:**
Debouncing delays a function's execution until after a specified time has passed **without it being called again** — useful for search inputs, resize events, etc., to avoid excessive calls.

```javascript
function debounce(fn, delay) {
  let timer;
  return function (...args) {
    clearTimeout(timer);
    timer = setTimeout(() => fn.apply(this, args), delay);
  };
}

const handleSearch = debounce((query) => {
  console.log("Searching for:", query);
}, 500);

// Rapid calls - only the LAST one (after 500ms of silence) actually runs
handleSearch("a");
handleSearch("ap");
handleSearch("app"); // only this triggers the search, after 500ms
```

---

## Q17. What is throttling?

**Answer:**
Throttling ensures a function runs **at most once** per specified time interval, regardless of how many times it's triggered — useful for scroll events, button clicks, etc.

```javascript
function throttle(fn, limit) {
  let inThrottle = false;
  return function (...args) {
    if (!inThrottle) {
      fn.apply(this, args);
      inThrottle = true;
      setTimeout(() => (inThrottle = false), limit);
    }
  };
}

const handleScroll = throttle(() => {
  console.log("Scroll event handled");
}, 1000);

window.addEventListener("scroll", handleScroll);
// Fires at most once every 1000ms, no matter how fast the user scrolls
```

**Debounce vs Throttle:**

| Feature | Debounce | Throttle |
|---------|----------|----------|
| Trigger | After a pause in activity | At regular intervals during activity |
| Use Case | Search-as-you-type, form validation | Scroll, resize, mouse-move handlers |

---

## Q18. What is the difference between `Promise.resolve()` and `new Promise()`?

**Answer:**
```javascript
// new Promise() - for wrapping async work (callbacks, timers, etc.)
const p1 = new Promise((resolve) => {
  setTimeout(() => resolve("done"), 1000);
});

// Promise.resolve() - shortcut to create an already-resolved Promise
const p2 = Promise.resolve("done immediately");

// Useful for normalizing values that might or might not be Promises
function ensurePromise(value) {
  return Promise.resolve(value); // wraps non-promise values safely
}
```

---

## Q19. What happens if you don't handle a Promise rejection?

**Answer:**
An unhandled rejection triggers an `unhandledrejection` event (browser) or a warning/crash in Node.js, and can silently fail without any error visible to the user.

```javascript
// ❌ No .catch() - unhandled rejection
fetch("/bad-url").then(res => res.json());

// ✅ Always handle rejections
fetch("/bad-url")
  .then(res => res.json())
  .catch(err => console.error("Request failed:", err));

// In async/await, always wrap in try/catch
async function run() {
  try {
    await fetch("/bad-url");
  } catch (err) {
    console.error(err);
  }
}
```

---

## Q20. What is the difference between `process.nextTick()`, microtasks, and `setImmediate()` in Node.js?

**Answer:**

| Queue | Priority | Example |
|-------|----------|---------|
| `process.nextTick()` | Highest — runs before other microtasks | Node.js only |
| Microtasks (Promise) | High — after `nextTick`, before macrotasks | `.then()`, `queueMicrotask()` |
| `setImmediate()` | Runs after I/O events in the current loop phase | Node.js only |
| `setTimeout(fn, 0)` | Macrotask — timer phase | Cross-platform |

```javascript
console.log("start");

setTimeout(() => console.log("setTimeout"), 0);
setImmediate(() => console.log("setImmediate"));
process.nextTick(() => console.log("nextTick"));
Promise.resolve().then(() => console.log("promise"));

console.log("end");

// Typical order: start, end, nextTick, promise, setTimeout/setImmediate (order can vary)
```

> **Interview Tip:** `process.nextTick()` and `setImmediate()` are Node.js-specific APIs — they don't exist in browsers.

---

# 💼 Common Interview Follow-up Questions

### 1. Is JavaScript single-threaded or multi-threaded?

JavaScript itself runs on a **single thread** (one call stack), but the runtime environment (browser or Node.js) provides Web APIs / libuv thread pools that handle async operations (timers, network requests, file I/O) outside that thread, feeding results back via the event loop and task queues.

### 2. Why does `setTimeout(fn, 0)` not run immediately?

Because `setTimeout` schedules a **macrotask**. Even with a 0ms delay, the callback must wait for: (1) the current synchronous code to finish, and (2) all queued microtasks to be processed first.

### 3. What is an `AbortController` used for?

It cancels in-progress async operations, most commonly `fetch()` requests.

```javascript
const controller = new AbortController();
const timeoutId = setTimeout(() => controller.abort(), 5000);

fetch(url, { signal: controller.signal })
  .then(res => res.json())
  .catch(err => {
    if (err.name === "AbortError") console.log("Request timed out");
  })
  .finally(() => clearTimeout(timeoutId));
```

### 4. Can you `await` a non-Promise value?

Yes — `await` on a non-Promise value simply resolves to that value immediately (it's implicitly wrapped in `Promise.resolve()`).

```javascript
async function test() {
  const value = await 42; // not a Promise, resolves instantly
  console.log(value); // 42
}
```

### 5. How would you retry a failed async request?

```javascript
async function fetchWithRetry(url, retries = 3, delay = 1000) {
  for (let attempt = 1; attempt <= retries; attempt++) {
    try {
      const response = await fetch(url);
      if (!response.ok) throw new Error(`Status ${response.status}`);
      return await response.json();
    } catch (err) {
      if (attempt === retries) throw err;
      await new Promise(resolve => setTimeout(resolve, delay));
    }
  }
}
```

### 6. What's the difference between concurrency and parallelism in JS?

- **Concurrency**: Multiple tasks make progress by interleaving on a single thread (JS's model via the event loop) — not truly simultaneous.
- **Parallelism**: Multiple tasks run at literally the same time on different threads/cores (e.g., Web Workers, Node.js worker threads).

### 7. How do you cancel a `setInterval` from within itself?

```javascript
let count = 0;
const id = setInterval(function () {
  console.log(++count);
  if (count >= 5) clearInterval(id);
}, 1000);
```

### 8. What is a "thenable"?

Any object with a `.then()` method — Promises are the most common thenable, but custom objects can implement the same interface and still work with `await` and `.then()` chains.

```javascript
const thenable = {
  then(resolve, reject) {
    resolve("Custom thenable resolved");
  },
};

await thenable; // works just like a real Promise
```

### 9. What does `Promise.all()` do if the array is empty?

It resolves immediately with an empty array `[]`, since there's nothing to wait for.

### 10. How do async functions interact with `try/catch/finally`?

`try` wraps the awaited call, `catch` handles rejection, and `finally` always runs — regardless of success or failure — making it ideal for cleanup (closing loaders, releasing resources).

```javascript
async function loadData() {
  showLoader();
  try {
    return await fetchData();
  } catch (err) {
    showError(err);
  } finally {
    hideLoader(); // always runs
  }
}
```

---
