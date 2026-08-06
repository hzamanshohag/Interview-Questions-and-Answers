# 📚 01 — JavaScript Fundamentals

## Topics Covered
- Variables
- Data Types
- Functions
- Scope

---

## Q1. What is the difference between `var`, `let`, and `const`?

**Answer:**

| Feature | `var` | `let` | `const` |
|---------|-------|-------|---------|
| Scope | Function | Block | Block |
| Redeclare | ✅ Yes | ❌ No | ❌ No |
| Reassign | ✅ Yes | ✅ Yes | ❌ No |
| Hoisted | ✅ Yes (initialized as `undefined`) | ✅ Yes (TDZ) | ✅ Yes (TDZ) |

**Example:**

```javascript
var a = 10;
let b = 20;
const c = 30;

a = 15;
b = 25;
// c = 35; // Error
```

---

## Q2. Explain the concept of hoisting in JavaScript.

**Answer:**

Hoisting is JavaScript's behavior of moving declarations to the top of their scope before execution.

- `var` is hoisted and initialized with `undefined`.
- `let` and `const` are hoisted but remain in the **Temporal Dead Zone (TDZ)** until initialized.
- Function declarations are fully hoisted.

**Example:**

```javascript
console.log(a); // undefined
var a = 10;

console.log(b); // ReferenceError
let b = 20;
```

---

## Q3. What are the primitive data types in JavaScript?

**Answer:**

JavaScript has **7 primitive data types**:

- String
- Number
- Boolean
- Undefined
- Null
- Symbol
- BigInt

**Example:**

```javascript
let name = "Shohag";
let age = 24;
let isDeveloper = true;
let salary;
let data = null;
let id = Symbol("id");
let big = 12345678901234567890n;
```

---

## Q4. What is the difference between `==` and `===` in JavaScript?

**Answer:**

- `==` compares values after type conversion.
- `===` compares both value and data type.

**Example:**

```javascript
5 == "5";   // true
5 === "5";  // false
```

Always prefer **`===`** for safer comparisons.

---

## Q5. Explain how closures work in JavaScript with an example.

**Answer:**

A closure is a function that remembers variables from its outer scope even after the outer function has finished executing.

**Example:**

```javascript
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
```

---

## Q6. What is the difference between `null` and `undefined`?

**Answer:**

| `null` | `undefined` |
|---------|-------------|
| Intentional empty value | Variable declared but not assigned |
| Type: object | Type: undefined |

**Example:**

```javascript
let a;
console.log(a); // undefined

let b = null;
console.log(b); // null
```

---

## Q7. What are arrow functions and how do they differ from regular functions?

**Answer:**

Arrow functions provide a shorter syntax and do not have their own `this`.

**Example:**

```javascript
// Regular Function
function greet(name) {
  return `Hello ${name}`;
}

// Arrow Function
const greet = (name) => `Hello ${name}`;
```

**Differences**

- Shorter syntax
- No own `this`
- Cannot be used as constructors
- No `arguments` object

---

## Q8. What is the scope chain in JavaScript?

**Answer:**

The scope chain is the process JavaScript uses to find variables by searching:

1. Local Scope
2. Parent Scope
3. Global Scope

**Example:**

```javascript
const name = "JavaScript";

function outer() {
  function inner() {
    console.log(name);
  }
  inner();
}

outer();
```

---

## Q9. Explain the concept of the Temporal Dead Zone (TDZ).

**Answer:**

The TDZ is the period between entering a block and declaring a `let` or `const` variable.

Accessing the variable before initialization causes a **ReferenceError**.

**Example:**

```javascript
console.log(a);

let a = 10;
```

---

## Q10. What is a pure function? Give an example.

**Answer:**

A pure function:

- Always returns the same output for the same input.
- Has no side effects.

**Example:**

```javascript
function add(a, b) {
  return a + b;
}
```

---

## Q11. What is the difference between function declaration and function expression?

**Answer:**

### Function Declaration

```javascript
function greet() {
  console.log("Hello");
}
```

- Hoisted completely.

### Function Expression

```javascript
const greet = function () {
  console.log("Hello");
};
```

- Not fully hoisted.

---

## Q12. What are default parameters in JavaScript?

**Answer:**

Default parameters provide default values if no argument is passed.

**Example:**

```javascript
function greet(name = "Guest") {
  return `Hello ${name}`;
}

greet();
```

Output:

```
Hello Guest
```

---

## Q13. What is the `typeof` operator and what are its possible return values?

**Answer:**

`typeof` returns the data type of a value.

**Common Results**

```javascript
typeof "Hello";      // string
typeof 10;           // number
typeof true;         // boolean
typeof undefined;    // undefined
typeof Symbol();     // symbol
typeof 10n;          // bigint
typeof {};           // object
typeof [];           // object
typeof function(){}; // function
```

---

## Q14. Explain type coercion in JavaScript with examples.

**Answer:**

Type coercion is JavaScript's automatic conversion of one data type into another.

**Examples:**

```javascript
"5" + 2
// "52"

"5" - 2
// 3

true + 1
// 2
```

Explicit conversion:

```javascript
Number("10");
String(10);
Boolean(1);
```

---

## Q15. What is an Immediately Invoked Function Expression (IIFE)?

**Answer:**

An IIFE is a function that executes immediately after it is defined.

**Example:**

```javascript
(function () {
  console.log("Executed immediately");
})();
```

Arrow Function IIFE:

```javascript
(() => {
  console.log("Hello");
})();
```

---

# 🎯 Day 1 Complete

**Topics Learned**

- Variables
- Data Types
- Scope
- Hoisting
- Closures
- Functions
- Pure Functions
- Type Coercion
- IIFE
- Arrow Functions
