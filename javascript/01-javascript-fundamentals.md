# 📚 01 — JavaScript Fundamentals

## 📖 Topics Covered

- Variables (`var`, `let`, `const`)
- Primitive Data Types
- Functions
- Scope & Scope Chain
- Hoisting
- Closures
- `null` vs `undefined`
- Arrow Functions
- Temporal Dead Zone (TDZ)
- Pure Functions
- Function Declaration vs Function Expression
- Default Parameters
- `typeof` Operator
- Type Coercion
- Immediately Invoked Function Expressions (IIFE)

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

## Q16. What is the difference between global scope, function scope, and block scope?

**Answer:**

JavaScript has three main types of scope:

- **Global Scope:** Variables are accessible from anywhere.
- **Function Scope:** Variables declared with `var` inside a function are only accessible within that function.
- **Block Scope:** Variables declared with `let` and `const` inside `{}` are only accessible within that block.

**Example:**

```javascript
const globalVar = "Global";

function demo() {
  var functionVar = "Function";

  if (true) {
    let blockVar = "Block";
    console.log(blockVar);
  }

  console.log(functionVar);
}

demo();
```

---

## Q17. What is the difference between mutable and immutable data?

**Answer:**

- **Mutable:** Can be changed after creation.
- **Immutable:** Cannot be changed after creation.

| Mutable | Immutable |
|---------|-----------|
| Objects | Strings |
| Arrays | Numbers |
| Functions | Booleans |

**Example:**

```javascript
const arr = [1, 2];
arr.push(3); // Mutable

const str = "Hello";
str[0] = "h"; // No effect
```

---

## Q18. What is the difference between pass by value and pass by reference?

**Answer:**

- Primitive values are passed **by value**.
- Objects and arrays are passed **by reference**.

**Example:**

```javascript
let a = 10;
let b = a;

b = 20;

console.log(a); // 10

const user = {
  name: "John"
};

const copy = user;

copy.name = "Shohag";

console.log(user.name); // Shohag
```

---

## Q19. What are truthy and falsy values in JavaScript?

**Answer:**

### Falsy Values

- false
- 0
- -0
- ""
- null
- undefined
- NaN

Everything else is **truthy**.

**Example:**

```javascript
if ("Hello") {
  console.log("Truthy");
}

if (0) {
  console.log("Won't execute");
}
```

---

## Q20. What is the difference between `undefined`, `null`, and `NaN`?

**Answer:**

| Value | Meaning |
|--------|---------|
| undefined | Variable declared but not assigned |
| null | Intentionally empty value |
| NaN | Invalid numeric result |

**Example:**

```javascript
let a;

console.log(a);

let b = null;

console.log(b);

console.log(Number("Hello"));
```

---

## Q21. What is the difference between `call()`, `apply()`, and `bind()`?

**Answer:**

These methods control the value of `this`.

| Method | Executes Immediately | Arguments |
|---------|----------------------|-----------|
| call() | ✅ | Comma separated |
| apply() | ✅ | Array |
| bind() | ❌ | Returns new function |

**Example:**

```javascript
const person = {
  name: "Shohag"
};

function greet(city) {
  console.log(`${this.name} from ${city}`);
}

greet.call(person, "Dhaka");
greet.apply(person, ["Khulna"]);

const fn = greet.bind(person);

fn("Jessore");
```

---

## Q22. What is the difference between `map()`, `filter()`, and `forEach()`?

**Answer:**

| Method | Returns New Array | Purpose |
|---------|------------------|---------|
| map() | ✅ | Transform data |
| filter() | ✅ | Filter data |
| forEach() | ❌ | Iterate only |

**Example:**

```javascript
const numbers = [1, 2, 3];

numbers.map(num => num * 2);

numbers.filter(num => num > 1);

numbers.forEach(num => console.log(num));
```

---

## Q23. What are template literals?

**Answer:**

Template literals use backticks (`` ` ``) and allow string interpolation.

**Example:**

```javascript
const name = "Shohag";

console.log(`Hello ${name}`);
```

---

## Q24. What is destructuring in JavaScript?

**Answer:**

Destructuring allows extracting values from arrays or objects.

**Example:**

```javascript
const user = {
  name: "Shohag",
  age: 24
};

const { name, age } = user;

const numbers = [10, 20];

const [a, b] = numbers;
```

---

## Q25. What is the difference between the spread operator (`...`) and the rest operator (`...`)?

**Answer:**

Although both use `...`, they serve different purposes.

### Spread Operator

Expands an array or object.

```javascript
const arr1 = [1, 2];

const arr2 = [...arr1, 3];
```

### Rest Operator

Collects multiple values into one array.

```javascript
function sum(...numbers) {
  return numbers.reduce((a, b) => a + b, 0);
}

sum(1, 2, 3, 4);
```

---

# 💼 Common Interview Follow-up Questions

These questions are frequently asked after JavaScript fundamentals:

- Explain lexical scope.
- What is the execution context?
- What is the difference between compile time and runtime?
- Why is JavaScript called a single-threaded language?
- What is the event loop?
- What are callback functions?
- What is callback hell?
- What are higher-order functions?
- What is a first-class function?
- Explain the `this` keyword with examples.
- What are factory functions?
- What are constructor functions?
- What is object cloning?
- What is optional chaining (`?.`)?
- What is the nullish coalescing operator (`??`)?
