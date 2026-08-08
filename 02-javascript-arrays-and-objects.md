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

