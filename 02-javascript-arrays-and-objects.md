# 📚 Day 2 — JavaScript Fundamentals II

### Topic: Arrays, Objects, ES6+ & Asynchronous JavaScript

---

## Q16. What is destructuring in JavaScript? Explain array and object destructuring with examples.

### Answer:

**Destructuring** is an ES6 feature that allows us to extract values from arrays or properties from objects and assign them to variables in a concise way.

There are two main types:

* Array destructuring
* Object destructuring

### Array Destructuring

Array destructuring extracts values based on their **position**.

```javascript
const colors = ["Red", "Green", "Blue"];

const [first, second, third] = colors;

console.log(first);  // Red
console.log(second); // Green
console.log(third);  // Blue
```

### Skipping Values

```javascript
const colors = ["Red", "Green", "Blue"];

const [, , third] = colors;

console.log(third); // Blue
```

### Default Values

```javascript
const [name = "Shohag", age = 24] = ["Hasan"];

console.log(name); // Hasan
console.log(age);  // 24
```

### Object Destructuring

Object destructuring extracts properties based on their **property names**.

```javascript
const user = {
  name: "Shohag",
  age: 24,
  profession: "Developer",
};

const { name, age } = user;

console.log(name); // Shohag
console.log(age);  // 24
```

### Renaming Properties

```javascript
const user = {
  name: "Shohag",
};

const { name: userName } = user;

console.log(userName); // Shohag
```

### Nested Destructuring

```javascript
const user = {
  name: "Shohag",
  address: {
    city: "Khulna",
  },
};

const {
  address: { city },
} = user;

console.log(city); // Khulna
```

### Interview Tip

> Array destructuring works based on **position**, while object destructuring works based on **property name**.

---

# Q17. What are the spread (`...`) and rest (`...`) operators in JavaScript?

### Answer:

Both **spread** and **rest** use the same `...` syntax, but they perform opposite operations.

* **Spread** → expands values.
* **Rest** → collects values.

---

### Spread Operator

The spread operator expands an iterable or object into individual elements/properties.

### Copying an Array

```javascript
const numbers = [1, 2, 3];

const copy = [...numbers];

console.log(copy); // [1, 2, 3]
```

### Merging Arrays

```javascript
const first = [1, 2];
const second = [3, 4];

const merged = [...first, ...second];

console.log(merged);
// [1, 2, 3, 4]
```

### Copying an Object

```javascript
const user = {
  name: "Shohag",
  age: 24,
};

const copy = { ...user };

console.log(copy);
```

### Adding Properties

```javascript
const user = {
  name: "Shohag",
};

const updatedUser = {
  ...user,
  age: 24,
};

console.log(updatedUser);
```

### Function Arguments

```javascript
function sum(a, b, c) {
  return a + b + c;
}

const numbers = [10, 20, 30];

console.log(sum(...numbers));
// 60
```

---

### Rest Operator

The rest operator collects multiple values into an array or object.

### Function Parameters

```javascript
function sum(...numbers) {
  return numbers.reduce((total, number) => total + number, 0);
}

console.log(sum(1, 2, 3, 4));
// 10
```

### Array Destructuring

```javascript
const numbers = [1, 2, 3, 4];

const [first, ...rest] = numbers;

console.log(first); // 1
console.log(rest);  // [2, 3, 4]
```

### Object Destructuring

```javascript
const user = {
  name: "Shohag",
  age: 24,
  city: "Khulna",
};

const { name, ...others } = user;

console.log(name);
// Shohag

console.log(others);
// { age: 24, city: "Khulna" }
```

### Interview Tip

> **Spread expands**, while **rest collects**.

---

# Q18. What is the difference between `map()`, `filter()`, and `reduce()`?

### Answer:

These are commonly used array methods, but they have different purposes.

| Method     | Purpose                        | Return       |
| ---------- | ------------------------------ | ------------ |
| `map()`    | Transform every element        | New array    |
| `filter()` | Select matching elements       | New array    |
| `reduce()` | Combine values into one result | Single value |

### `map()`

`map()` creates a new array by transforming every element.

```javascript
const numbers = [1, 2, 3, 4];

const doubled = numbers.map(number => number * 2);

console.log(doubled);
// [2, 4, 6, 8]
```

### `filter()`

`filter()` creates a new array containing elements that satisfy a condition.

```javascript
const numbers = [1, 2, 3, 4, 5];

const evenNumbers = numbers.filter(number => number % 2 === 0);

console.log(evenNumbers);
// [2, 4]
```

### `reduce()`

`reduce()` combines array elements into a single accumulated result.

```javascript
const numbers = [1, 2, 3, 4];

const sum = numbers.reduce(
  (total, number) => total + number,
  0
);

console.log(sum);
// 10
```

### Practical Example

```javascript
const products = [
  { name: "Laptop", price: 70000 },
  { name: "Mouse", price: 1000 },
  { name: "Keyboard", price: 2000 },
];

const names = products.map(product => product.name);

const expensive = products.filter(product => product.price > 5000);

const total = products.reduce(
  (sum, product) => sum + product.price,
  0
);
```

### Interview Tip

> Use `map()` to **transform**, `filter()` to **select**, and `reduce()` to **accumulate**.

---

# Q19. What is the difference between `for...in` and `for...of` loops?

### Answer:

The main difference is what they iterate over.

* `for...in` → iterates over **keys/property names**.
* `for...of` → iterates over **values** of an iterable.

### `for...in`

```javascript
const user = {
  name: "Shohag",
  age: 24,
};

for (const key in user) {
  console.log(key, user[key]);
}
```

Output:

```text
name Shohag
age 24
```

### `for...of`

```javascript
const numbers = [10, 20, 30];

for (const number of numbers) {
  console.log(number);
}
```

Output:

```text
10
20
30
```

### Comparison

| Feature            | `for...in`             | `for...of`                  |
| ------------------ | ---------------------- | --------------------------- |
| Iterates           | Keys                   | Values                      |
| Commonly used with | Objects                | Arrays, strings, Maps, Sets |
| Returns            | Property names/indexes | Actual values               |

### Important Example

```javascript
const numbers = [10, 20, 30];

for (const index in numbers) {
  console.log(index);
}

// 0
// 1
// 2

for (const value of numbers) {
  console.log(value);
}

// 10
// 20
// 30
```

### Interview Tip

> Remember: **`in` = keys**, **`of` = values**.

---

# Q20. What are template literals and tagged templates?

### Answer:

**Template literals** are strings created using backticks `` ` `` instead of single or double quotes.

They allow:

* String interpolation
* Multi-line strings
* Embedded expressions

### String Interpolation

```javascript
const name = "Shohag";
const age = 24;

const message = `My name is ${name} and I am ${age} years old.`;

console.log(message);
```

### Expressions

```javascript
const a = 10;
const b = 20;

console.log(`The result is ${a + b}`);
// The result is 30
```

### Multi-line Strings

```javascript
const message = `
Hello Shohag,
Welcome to JavaScript.
Good luck with your interview!
`;

console.log(message);
```

### Tagged Templates

A **tagged template** allows a function to process a template literal.

```javascript
function highlight(strings, name) {
  return `${strings[0]}${name.toUpperCase()}${strings[1]}`;
}

const name = "Shohag";

const result = highlight`Hello ${name}!`;

console.log(result);
// Hello SHOHAG!
```

### Interview Tip

> Template literals improve string readability and make dynamic strings easier to create.

---

# Q21. What is the JavaScript Event Loop?

### Answer:

The **Event Loop** is the mechanism that allows JavaScript to handle asynchronous operations even though JavaScript runs code on a single main thread.

JavaScript uses:

* Call Stack
* Web APIs / Runtime APIs
* Task Queue
* Microtask Queue
* Event Loop

### Basic Flow

```text
JavaScript Code
      ↓
  Call Stack
      ↓
Web APIs / Async Operations
      ↓
Task / Microtask Queues
      ↓
  Event Loop
      ↓
  Call Stack
```

### Example

```javascript
console.log("Start");

setTimeout(() => {
  console.log("Timeout");
}, 0);

console.log("End");
```

Output:

```text
Start
End
Timeout
```

Even though the timeout is `0ms`, its callback does not execute immediately. It waits until the current synchronous code finishes.

### Promise Example

```javascript
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

Promises use the **microtask queue**, which is processed before the regular task queue.

### Interview Tip

> The Event Loop continuously checks whether the Call Stack is empty and then moves eligible asynchronous callbacks from the queues to the Call Stack.

---

# Q22. What are Promises in JavaScript?

### Answer:

A **Promise** is an object that represents the eventual result of an asynchronous operation.

A Promise has three states:

1. **Pending** → operation is still running.
2. **Fulfilled** → operation completed successfully.
3. **Rejected** → operation failed.

```text
Pending
  ↓
  ├── Fulfilled
  │
  └── Rejected
```

### Creating a Promise

```javascript
const promise = new Promise((resolve, reject) => {
  const success = true;

  if (success) {
    resolve("Operation successful");
  } else {
    reject("Operation failed");
  }
});
```

### Consuming a Promise

```javascript
promise
  .then(result => {
    console.log(result);
  })
  .catch(error => {
    console.log(error);
  })
  .finally(() => {
    console.log("Finished");
  });
```

### Real-World Example

```javascript
fetch("https://api.example.com/users")
  .then(response => response.json())
  .then(data => {
    console.log(data);
  })
  .catch(error => {
    console.error(error);
  });
```

### Interview Tip

> Promises help manage asynchronous operations and avoid deeply nested callback structures.

---

# Q23. What is `async/await` and how does it improve upon Promises?

### Answer:

`async/await` is syntax built on top of Promises that makes asynchronous code easier to read and write.

An `async` function always returns a Promise.

`await` pauses execution inside the async function until the Promise settles.

### Promise Syntax

```javascript
fetch("/api/users")
  .then(response => response.json())
  .then(data => {
    console.log(data);
  })
  .catch(error => {
    console.error(error);
  });
```

### Async/Await Syntax

```javascript
async function getUsers() {
  try {
    const response = await fetch("/api/users");

    const data = await response.json();

    console.log(data);
  } catch (error) {
    console.error(error);
  }
}

getUsers();
```

### Advantages

* Easier to read
* Easier error handling
* Looks similar to synchronous code
* Reduces `.then()` chaining
* Makes complex asynchronous workflows easier to understand

### Important Point

`await` does **not** block the entire JavaScript thread. It pauses the execution of that particular async function while other JavaScript work can continue.

### Interview Tip

> `async/await` doesn't replace Promises; it provides a cleaner syntax for working with them.

---

# Q24. What is the difference between `call()`, `apply()`, and `bind()`?

### Answer:

`call()`, `apply()`, and `bind()` are used to control the value of `this` when calling a function.

### `call()`

`call()` invokes the function immediately and accepts arguments individually.

```javascript
function introduce(city, country) {
  console.log(
    `${this.name} lives in ${city}, ${country}`
  );
}

const user = {
  name: "Shohag",
};

introduce.call(user, "Khulna", "Bangladesh");
```

### `apply()`

`apply()` also invokes the function immediately, but arguments are passed as an array.

```javascript
introduce.apply(user, ["Khulna", "Bangladesh"]);
```

### `bind()`

`bind()` does not immediately execute the function.

Instead, it returns a new function with the specified `this` value.

```javascript
const boundIntroduce = introduce.bind(
  user,
  "Khulna",
  "Bangladesh"
);

boundIntroduce();
```

### Comparison

| Method    | Executes Immediately? | Arguments            |
| --------- | --------------------- | -------------------- |
| `call()`  | Yes                   | Individual arguments |
| `apply()` | Yes                   | Array                |
| `bind()`  | No                    | Individual arguments |

### Interview Tip

> `call()` and `apply()` **call now**. `bind()` **returns a function for later**.

---

# Q25. What is prototypal inheritance in JavaScript?

### Answer:

**Prototypal inheritance** is the mechanism JavaScript uses for objects to inherit properties and methods from other objects through the **prototype chain**.

Every JavaScript object has an internal prototype reference.

### Example

```javascript
const person = {
  greet() {
    console.log("Hello");
  },
};

const user = Object.create(person);

user.greet();
```

Here, `user` doesn't directly contain `greet()`. JavaScript searches the prototype chain and finds it in `person`.

### Prototype Chain

```text
user
  ↓
person
  ↓
Object.prototype
  ↓
null
```

### Constructor Example

```javascript
function Person(name) {
  this.name = name;
}

Person.prototype.greet = function () {
  console.log(`Hello, ${this.name}`);
};

const user = new Person("Shohag");

user.greet();
```

The `greet()` method is stored on `Person.prototype`, so instances can share the same method.

### Class Syntax

Modern JavaScript provides `class` syntax, but classes still use prototypes internally.

```javascript
class Person {
  constructor(name) {
    this.name = name;
  }

  greet() {
    console.log(`Hello, ${this.name}`);
  }
}
```

### Interview Tip

> JavaScript uses **prototype-based inheritance**, and `class` is primarily a more convenient syntax built on top of that system.

---

# Q26. What is the `this` keyword in JavaScript?

### Answer:

`this` refers to a value determined by **how a function is called**.

Its value can change depending on the execution context.

### 1. Object Method

```javascript
const user = {
  name: "Shohag",

  greet() {
    console.log(this.name);
  },
};

user.greet();
// Shohag
```

Here, `this` refers to `user`.

### 2. Regular Function

In strict mode, a regular function called without an owner has:

```javascript
this === undefined
```

```javascript
"use strict";

function test() {
  console.log(this);
}

test();
// undefined
```

### 3. Constructor

When using `new`, `this` refers to the newly created object.

```javascript
function User(name) {
  this.name = name;
}

const user = new User("Shohag");

console.log(user.name);
// Shohag
```

### 4. Arrow Function

Arrow functions do not create their own `this`. They inherit `this` from their surrounding lexical scope.

```javascript
const user = {
  name: "Shohag",

  greet: function () {
    const inner = () => {
      console.log(this.name);
    };

    inner();
  },
};

user.greet();
// Shohag
```

### 5. Explicit Binding

`call()`, `apply()`, and `bind()` can explicitly control `this`.

```javascript
function greet() {
  console.log(this.name);
}

const user = {
  name: "Shohag",
};

greet.call(user);
// Shohag
```

### Interview Tip

> The value of `this` is primarily determined by **how a function is invoked**, while arrow functions inherit `this` from their surrounding scope.

---

