# JavaScript Core Language & Execution

JavaScript-এর **Hoisting, TDZ, Execution Context, Event Loop, Scope, Closure, `this`, bind/call/apply, Currying এবং Function Composition** বোঝানো হয়েছে।

---

## 1. Hoisting কী? `var`, `let`, `const`, Function Declaration

**Hoisting** হলো JavaScript code execute করার আগে কিছু variable ও function declaration-এর তথ্য memory-তে রাখার behavior।

### `var`

`var` hoist হয় এবং শুরুতে তার value থাকে `undefined`।

```js
console.log(name); // undefined

var name = "Shohag";
```

JavaScript এটাকে প্রায় এমনভাবে দেখে:

```js
var name;
console.log(name); // undefined

name = "Shohag";
```

### `let`

`let`-ও hoist হয়, কিন্তু declaration-এর আগে access করা যায় না।

```js
console.log(age); // ReferenceError

let age = 25;
```

### `const`

`const`-এর ক্ষেত্রেও একই নিয়ম।

```js
console.log(country); // ReferenceError

const country = "Bangladesh";
```

### Function Declaration

Function declaration পুরোপুরি hoist হয়। তাই declaration-এর আগেও function call করা যায়।

```js
sayHello();

function sayHello() {
  console.log("Hello!");
}
```

**সহজভাবে মনে রাখুন:**

| Type | Hoisted? | Declaration-এর আগে access |
|---|---|---|
| `var` | Yes | `undefined` |
| `let` | Yes | ❌ ReferenceError |
| `const` | Yes | ❌ ReferenceError |
| Function Declaration | Yes | ✅ কাজ করে |

---

## 2. Temporal Dead Zone (TDZ) কী?

**TDZ** হলো variable declare হওয়ার শুরু থেকে declaration line পর্যন্ত সময়।

`let` এবং `const` এই সময়ের মধ্যে থাকে।

```js
console.log(name); // ReferenceError

let name = "Shohag";
```

এখানে `name` memory-তে আছে, কিন্তু এখনো initialize হয়নি। তাই access করলে error হয়।

### TDZ কেন আছে?

মূল উদ্দেশ্য হলো code-কে আরও predictable এবং safe করা।

যদি `let` বা `const` declaration-এর আগে ব্যবহার করা যেত, তাহলে অনেক confusing bug তৈরি হতে পারত।

```js
console.log(x); // ReferenceError

let x = 10;
```

---

## 3. JavaScript Execution Context কীভাবে কাজ করে?

**Execution Context** হলো এমন একটি environment যেখানে JavaScript code execute করে।

প্রধানত ৩ ধরনের context দেখা যায়:

1. **Global Execution Context**
2. **Function Execution Context**
3. **Eval Execution Context**

একটি function call হলে নতুন **Function Execution Context** তৈরি হয়।

### Execution Context-এর সহজ ধাপ

ধরুন:

```js
var name = "Shohag";

function hello() {
  console.log("Hello", name);
}

hello();
```

JavaScript সাধারণভাবে:

### Step 1 — Creation Phase

Memory-তে variables এবং functions-এর information রাখা হয়।

```text
name → undefined
hello → function
```

### Step 2 — Execution Phase

তারপর code line by line execute হয়।

```text
name → "Shohag"
hello() → function call
```

Function call হলে নতুন execution context তৈরি হয়।

```text
Global Context
      ↓
hello() Function Context
```

---

## 4. Call Stack, Task Queue এবং Microtask Queue

### Call Stack

**Call Stack** হলো যেখানে বর্তমানে execute হওয়া functionগুলো রাখা হয়।

```js
function one() {
  two();
}

function two() {
  console.log("Hello");
}

one();
```

Stack:

```text
two()
one()
global
```

`two()` শেষ হলে সেটা stack থেকে বের হয়ে যায়।

---

### Task Queue / Macrotask Queue

এখানে সাধারণত asynchronous task থাকে।

উদাহরণ:

```js
setTimeout(() => {
  console.log("Timer");
}, 0);
```

`setTimeout` callback পরে Task Queue-তে যায়।

---

### Microtask Queue

এখানে সাধারণত Promise-এর callback থাকে।

```js
Promise.resolve().then(() => {
  console.log("Promise");
});
```

Promise callback **Microtask Queue**-তে যায়।

### Priority

সহজভাবে:

```text
Call Stack
   ↓
Microtask Queue
   ↓
Task Queue
```

অর্থাৎ Microtask Queue সাধারণত Task Queue-এর আগে execute হয়।

---

## 5. Event Loop কীভাবে Promise-কে `setTimeout`-এর আগে চালায়?

এই code দেখুন:

```js
console.log("Start");

setTimeout(() => {
  console.log("Timeout");
}, 0);

Promise.resolve().then(() => {
  console.log("Promise");
});

console.log("End");
```

Output:

```text
Start
End
Promise
Timeout
```

### কেন?

প্রথমে synchronous code execute হয়:

```text
Start
End
```

তারপর Event Loop দেখে Microtask Queue-তে Promise আছে।

```text
Promise
```

তারপর Task Queue থেকে `setTimeout` callback execute হয়।

```text
Timeout
```

তাই:

```text
Synchronous Code
      ↓
Microtasks / Promise
      ↓
Tasks / setTimeout
```

---

## 6. Lexical Scoping কী?

**Lexical Scope** মানে কোনো variable কোথায় access করা যাবে সেটা code লেখার location-এর উপর নির্ভর করে।

```js
const name = "Shohag";

function hello() {
  console.log(name);
}

hello();
```

এখানে `hello()` function তার outer scope-এর `name` দেখতে পারে।

আরও একটি example:

```js
function outer() {
  const message = "Hello";

  function inner() {
    console.log(message);
  }

  inner();
}

outer();
```

`inner()` তার নিজের scope-এ `message` না পেলেও outer scope-এ খুঁজে পায়।

এটাই **Lexical Scoping**।

---

## 7. Undeclared Variable vs `undefined`

### `undefined`

Variable declare করা হয়েছে, কিন্তু value দেওয়া হয়নি।

```js
let name;

console.log(name); // undefined
```

এখানে `name` declared।

---

### Undeclared Variable

Variable declare-ই করা হয়নি।

```js
console.log(age);
```

এখানে `age` declare করা হয়নি।

Result:

```text
ReferenceError: age is not defined
```

### সহজভাবে

```text
Declared + no value = undefined

Not declared = ReferenceError
```

---

# Functions & Closures

## 8. Closure কী?

**Closure** হলো যখন একটি inner function তার outer function-এর variable মনে রাখে, এমনকি outer function শেষ হয়ে যাওয়ার পরও।

```js
function counter() {
  let count = 0;

  return function () {
    count++;
    return count;
  };
}

const increment = counter();

console.log(increment()); // 1
console.log(increment()); // 2
console.log(increment()); // 3
```

এখানে `counter()` শেষ হয়ে গেছে, কিন্তু returned function `count` variable-কে মনে রেখেছে।

এটাই Closure।

### Closure কখন Memory Leak তৈরি করতে পারে?

Closure নিজে memory leak নয়।

কিন্তু যদি কোনো closure অপ্রয়োজনীয় বড় object বা DOM element-এর reference ধরে রাখে এবং সেটা আর release না হয়, তাহলে memory বেশি ব্যবহার হতে পারে।

Example:

```js
function createHandler() {
  const hugeData = new Array(1000000);

  return function () {
    console.log(hugeData.length);
  };
}

const handler = createHandler();
```

যতক্ষণ `handler` alive থাকে, `hugeData`-ও memory-তে থাকতে পারে।

---

## 9. Function Declaration vs Function Expression

### Function Declaration

```js
function add(a, b) {
  return a + b;
}
```

এটি hoisted হয়।

```js
add(2, 3); // 5

function add(a, b) {
  return a + b;
}
```

---

### Function Expression

```js
const add = function (a, b) {
  return a + b;
};
```

এখানে function একটি variable-এর মধ্যে store করা হয়েছে।

Declaration-এর আগে call করলে কাজ করবে না।

```js
add(2, 3); // ReferenceError

const add = function (a, b) {
  return a + b;
};
```

---

## 10. `this` কীভাবে কাজ করে?

`this`-এর value নির্ভর করে **function কীভাবে call করা হয়েছে** তার উপর।

### Normal Function

```js
const user = {
  name: "Shohag",

  sayHello: function () {
    console.log(this.name);
  },
};

user.sayHello();
```

Output:

```text
Shohag
```

এখানে `this` হলো `user` object।

---

### Arrow Function

Arrow function নিজের `this` তৈরি করে না।

```js
const user = {
  name: "Shohag",

  sayHello: () => {
    console.log(this.name);
  },
};
```

এখানে `this` object-এর `user` হবে না।

Arrow function তার outer lexical `this` ব্যবহার করে।

---

### Event Handler

Browser event handler-এ সাধারণ function ব্যবহার করলে `this` সাধারণত যে element event receive করেছে সেটিকে নির্দেশ করে।

```js
button.addEventListener("click", function () {
  console.log(this);
});
```

এখানে `this` সাধারণত `button` element।

Arrow function ব্যবহার করলে:

```js
button.addEventListener("click", () => {
  console.log(this);
});
```

এখানে `this` event element-কে নির্দেশ করবে না; arrow function outer `this` ব্যবহার করবে।

---

## 11. `bind`, `call`, `apply`

এই তিনটি method দিয়ে function-এর `this` এবং arguments control করা যায়।

### `call()`

Function সঙ্গে সঙ্গে execute হয়।

```js
function greet(city) {
  console.log(this.name, city);
}

const user = {
  name: "Shohag",
};

greet.call(user, "Khulna");
```

---

### `apply()`

`call()`-এর মতো, কিন্তু arguments array হিসেবে দেওয়া হয়।

```js
greet.apply(user, ["Khulna"]);
```

### `bind()`

Function সঙ্গে সঙ্গে execute করে না। নতুন একটি function return করে।

```js
const newGreet = greet.bind(user, "Khulna");

newGreet();
```

### সহজভাবে

```text
call  → এখনই call করে
apply → এখনই call করে + arguments array
bind  → নতুন function তৈরি করে
```

---

## 12. Currying কী?

**Currying** হলো একটি function-এর multiple arguments-কে একসাথে না নিয়ে একবারে একটি করে argument নেওয়ার technique।

Normal function:

```js
function add(a, b, c) {
  return a + b + c;
}

add(1, 2, 3);
```

Curried version:

```js
function add(a) {
  return function (b) {
    return function (c) {
      return a + b + c;
    };
  };
}

console.log(add(1)(2)(3)); // 6
```

### কেন useful?

Currying দিয়ে reusable function তৈরি করা সহজ হয়।

```js
const add10 = add(10);

console.log(add10(20)(30));
```

এটি functional programming-এ অনেক useful।

---

## 13. Function Composition কী?

**Function Composition** হলো একাধিক ছোট function একসাথে combine করে একটি নতুন function তৈরি করা।

ধরুন:

```js
const add = (x) => x + 10;

const multiply = (x) => x * 2;
```

এখন:

```js
const result = multiply(add(5));

console.log(result); // 30
```

কারণ:

```text
5
 ↓
add(5)
 ↓
15
 ↓
multiply(15)
 ↓
30
```

### সহজ উদাহরণ

```js
const trim = (text) => text.trim();

const upper = (text) => text.toUpperCase();

const addBang = (text) => text + "!";

const result = addBang(upper(trim(" hello ")));

console.log(result);
// HELLO!
```

এখানে ছোট ছোট function একসাথে কাজ করছে।

### Composition-এর সুবিধা

- Code ছোট ও reusable হয়
- Function আলাদা করে test করা যায়
- Complex logic ছোট ছোট অংশে ভাগ করা যায়
- Functional programming-এ খুব useful

---

# Quick Revision

```text
Hoisting
→ Declaration আগে memory-তে যায়

var
→ আগে access করলে undefined

let / const
→ আগে access করলে ReferenceError (TDZ)

Function Declaration
→ পুরোপুরি hoisted

Execution Context
→ যেখানে JavaScript code execute হয়

Call Stack
→ বর্তমানে চলা function রাখে

Microtask Queue
→ Promise callback

Task Queue
→ setTimeout callback

Event Loop
→ Stack খালি হলে আগে Microtask, পরে Task দেখে

Lexical Scope
→ Code কোথায় লেখা হয়েছে তার উপর scope নির্ভর করে

undefined
→ Variable declared, value নেই

Undeclared
→ Variable declare করা হয়নি

Closure
→ Inner function outer variable মনে রাখে

this
→ Function কীভাবে call হয়েছে তার উপর নির্ভর করে

call
→ Immediately execute

apply
→ Immediately execute + arguments array

bind
→ নতুন function return করে

Currying
→ একবারে একটি argument নেওয়া

Composition
→ একাধিক function combine করা
```
