# 📚 02 — JavaScript Arrays and Objects

## 📖 Topics Covered
- Arrays
- Objects
- Array Methods
- Object Methods
- Array Iteration
- Object Iteration
- Destructuring
- Spread Operator (`...`)
- Rest Operator (`...`)
- Shallow Copy vs Deep Copy
- Optional Chaining (`?.`)
- Nullish Coalescing (`??`)
- Object Cloning
- Object Freezing & Sealing

---

## Q1. What is the difference between Arrays and Objects?

**Answer:**
Arrays and Objects are both used to store collections of data, but they serve different purposes.

- **Arrays** store ordered collections of values using numeric indexes.
- **Objects** store data as key-value pairs using property names.

| Feature | Array | Object |
|---------|-------|--------|
| Data Structure | Ordered collection | Key-value collection |
| Keys | Numeric indexes (0, 1, 2...) | Custom property names |
| Best Used For | Lists of similar data | Related data with properties |
| Access | `array[index]` | `object.key` or `object["key"]` |
| Built-in Methods | `map()`, `filter()`, `reduce()`, etc. | `Object.keys()`, `Object.values()`, `Object.entries()` |

**Example:**
```javascript
// Array
const fruits = ["Apple", "Banana", "Orange"];
console.log(fruits[0]); // Apple

// Object
const user = {
  name: "Shohag",
  age: 24,
  profession: "Full Stack Developer",
};
console.log(user.name); // Shohag
```

**When to Use**
- ✅ Use an **Array** when storing a list of similar items.
- ✅ Use an **Object** when storing information with named properties.

```javascript
// Good use of an Array
const colors = ["Red", "Green", "Blue"];

// Good use of an Object
const product = {
  id: 1,
  title: "Laptop",
  price: 75000,
};
```

> **Interview Tip:** Arrays are actually specialized objects in JavaScript, which is why `typeof []` returns `"object"`. To check whether a value is an array, use `Array.isArray()`.

```javascript
const arr = [1, 2, 3];
console.log(typeof arr); // "object"
console.log(Array.isArray(arr)); // true
```

---

## Q2. How do you create an array in JavaScript?

**Answer:**
There are several ways to create an array:

```javascript
// 1. Array literal (most common, preferred)
const arr1 = [1, 2, 3];

// 2. Array constructor
const arr2 = new Array(1, 2, 3);

// 3. Array constructor with a single number → creates empty array of that length
const arr3 = new Array(5); // [ <5 empty items> ]

// 4. Array.of() → creates array from arguments (avoids the single-number trap)
const arr4 = Array.of(5); // [5]

// 5. Array.from() → creates array from iterable or array-like object
const arr5 = Array.from("hello"); // ["h","e","l","l","o"]
const arr6 = Array.from({ length: 3 }, (_, i) => i * 2); // [0, 2, 4]
```

> **Interview Tip:** `new Array(5)` creates a sparse array with 5 empty slots, not `[5]`. This is a classic gotcha — prefer array literals or `Array.of()`/`Array.from()` for clarity.

---

## Q3. What are the most commonly used array methods?

**Answer:**

| Category | Methods |
|----------|---------|
| Add/Remove | `push()`, `pop()`, `shift()`, `unshift()`, `splice()` |
| Search | `indexOf()`, `includes()`, `find()`, `findIndex()` |
| Transform | `map()`, `filter()`, `reduce()`, `flat()`, `flatMap()` |
| Iterate | `forEach()`, `for...of` |
| Combine | `concat()`, spread `...` |
| Check | `every()`, `some()`, `Array.isArray()` |
| Sort/Reverse | `sort()`, `reverse()` |
| Convert | `join()`, `toString()`, `Array.from()` |
| Slice | `slice()` |

```javascript
const nums = [4, 2, 8, 6];

nums.push(10);            // [4,2,8,6,10]
nums.map(n => n * 2);     // [8,4,16,12,20]
nums.filter(n => n > 4);  // [8,6,10]
nums.find(n => n > 4);    // 8
nums.includes(6);         // true
nums.sort((a, b) => a - b); // [2,4,6,8,10]
```

---

## Q4. What is the difference between `map()`, `filter()`, `reduce()`, and `forEach()`?

**Answer:**

| Method | Returns | Use Case |
|--------|---------|----------|
| `map()` | New array (same length) | Transform each element |
| `filter()` | New array (subset) | Select elements matching a condition |
| `reduce()` | Single accumulated value | Combine elements into one result (sum, object, etc.) |
| `forEach()` | `undefined` | Run side effects (logging, DOM updates) — no new array |

```javascript
const nums = [1, 2, 3, 4, 5];

const doubled = nums.map(n => n * 2);        // [2,4,6,8,10]
const evens = nums.filter(n => n % 2 === 0); // [2,4]
const sum = nums.reduce((acc, n) => acc + n, 0); // 15

nums.forEach(n => console.log(n)); // logs each number, returns undefined
```

> **Interview Tip:** `forEach()` cannot be chained and cannot be stopped with `break`. If you need a new array, use `map()`/`filter()`; if you need side effects only, use `forEach()`.

---

## Q5. What is the difference between `find()` and `filter()`?

**Answer:**

| Method | Returns | Stops Early? |
|--------|---------|---------------|
| `find()` | First matching **element** (or `undefined`) | Yes |
| `filter()` | **Array** of all matching elements | No |

```javascript
const users = [
  { id: 1, active: false },
  { id: 2, active: true },
  { id: 3, active: true },
];

users.find(u => u.active);   // { id: 2, active: true }
users.filter(u => u.active); // [{id:2,...}, {id:3,...}]
```

---

## Q6. What is the difference between `slice()` and `splice()`?

**Answer:**

| Feature | `slice()` | `splice()` |
|---------|-----------|------------|
| Mutates original? | ❌ No | ✅ Yes |
| Returns | New array (copied portion) | Array of removed elements |
| Purpose | Extract a portion | Add/remove/replace elements |

```javascript
const arr = [1, 2, 3, 4, 5];

// slice(start, end) - end is exclusive, non-mutating
const sliced = arr.slice(1, 3); // [2, 3]
console.log(arr); // [1,2,3,4,5] (unchanged)

// splice(start, deleteCount, ...itemsToInsert) - mutating
const removed = arr.splice(1, 2, "a", "b"); // removes [2,3], inserts "a","b"
console.log(arr);     // [1, "a", "b", 4, 5]
console.log(removed); // [2, 3]
```

---

## Q7. What is the difference between `push()`, `pop()`, `shift()`, and `unshift()`?

**Answer:**

| Method | Action | End | Returns |
|--------|--------|-----|---------|
| `push()` | Add item(s) | End | New length |
| `pop()` | Remove item | End | Removed item |
| `shift()` | Remove item | Start | Removed item |
| `unshift()` | Add item(s) | Start | New length |

```javascript
const arr = [2, 3, 4];

arr.push(5);     // [2,3,4,5]
arr.pop();       // [2,3,4]
arr.unshift(1);  // [1,2,3,4]
arr.shift();     // [2,3,4]
```

> **Interview Tip:** `push()`/`pop()` operate at the end and are O(1) (fast). `shift()`/`unshift()` operate at the start and are O(n) because all other elements must be re-indexed.

---

## Q8. What is the difference between `concat()` and the spread operator?

**Answer:**
Both merge arrays without mutating the originals, but they differ in flexibility and syntax.

```javascript
const a = [1, 2];
const b = [3, 4];

// concat()
const merged1 = a.concat(b); // [1,2,3,4]

// spread operator
const merged2 = [...a, ...b]; // [1,2,3,4]

// spread is more flexible - can mix arrays, values, and insert anywhere
const merged3 = [0, ...a, 2.5, ...b, 5]; // [0,1,2,2.5,3,4,5]
```

> **Interview Tip:** Spread is generally preferred in modern code for readability and flexibility; `concat()` still works fine and can also accept non-array arguments as single values.

---

## Q9. How do you remove duplicate values from an array?

**Answer:**
The most common approach uses `Set`, which only stores unique values.

```javascript
const nums = [1, 2, 2, 3, 4, 4, 5];

const unique = [...new Set(nums)]; // [1,2,3,4,5]

// Alternative using filter()
const unique2 = nums.filter((n, index) => nums.indexOf(n) === index);
```

For arrays of objects, dedupe by a specific key:
```javascript
const users = [{ id: 1 }, { id: 2 }, { id: 1 }];
const uniqueUsers = [...new Map(users.map(u => [u.id, u])).values()];
```

---

## Q10. How do you sort an array of numbers?

**Answer:**
`sort()` mutates the array in place and, by default, sorts elements as **strings** — which breaks numeric order. A compare function is required for correct numeric sorting.

```javascript
const nums = [10, 2, 33, 4];

nums.sort();                     // [10, 2, 33, 4] → WRONG (string sort)
nums.sort((a, b) => a - b);      // [2, 4, 10, 33]  → ascending
nums.sort((a, b) => b - a);      // [33, 10, 4, 2]  → descending
```

> **Interview Tip:** `[10, 2, 33, 4].sort()` gives `[10, 2, 33, 4]` unchanged in some cases or wrong order in general — always pass a compare function for numbers.

---

## Q11. How do you merge two arrays?

**Answer:**
```javascript
const a = [1, 2];
const b = [3, 4];

// Using spread
const merged1 = [...a, ...b]; // [1,2,3,4]

// Using concat
const merged2 = a.concat(b); // [1,2,3,4]

// Merge and remove duplicates
const merged3 = [...new Set([...a, ...b])];
```

---

## Q12. How do you flatten a nested array?

**Answer:**
```javascript
const nested = [1, [2, 3], [4, [5, 6]]];

nested.flat();          // [1, 2, 3, 4, [5, 6]]  → 1 level deep
nested.flat(2);         // [1, 2, 3, 4, 5, 6]     → 2 levels deep
nested.flat(Infinity);  // fully flattens any depth

// flatMap() = map() + flat(1), useful when each mapped value is an array
[1, 2, 3].flatMap(n => [n, n * 2]); // [1,2, 2,4, 3,6]
```

---

## Q13. What is array destructuring?

**Answer:**
Array destructuring lets you unpack values from an array into individual variables based on position.

```javascript
const colors = ["Red", "Green", "Blue"];

const [first, second, third] = colors;
console.log(first, second, third); // Red Green Blue

// Skipping elements
const [, , onlyThird] = colors; // Blue

// Default values
const [a = "Yellow", b = "Purple"] = ["Orange"];
console.log(a, b); // Orange Purple

// Swapping variables
let x = 1, y = 2;
[x, y] = [y, x]; // x=2, y=1
```

---

## Q14. What is object destructuring?

**Answer:**
Object destructuring unpacks properties from an object into variables by matching property names.

```javascript
const user = { name: "Shohag", age: 24, profession: "Developer" };

const { name, age } = user;
console.log(name, age); // Shohag 24

// Renaming variables
const { name: userName } = user;
console.log(userName); // Shohag

// Default values
const { country = "Bangladesh" } = user;
console.log(country); // Bangladesh

// Nested destructuring
const profile = { name: "Shohag", address: { city: "Khulna" } };
const { address: { city } } = profile;
console.log(city); // Khulna
```

---

## Q15. What is the spread operator?

**Answer:**
The spread operator (`...`) expands an iterable (array, object, string) into its individual elements. It's used to copy, merge, or pass values.

```javascript
// Arrays
const arr = [1, 2, 3];
const copy = [...arr];          // [1,2,3] - shallow copy
const combined = [...arr, 4, 5]; // [1,2,3,4,5]

// Objects
const obj = { a: 1, b: 2 };
const objCopy = { ...obj };          // shallow copy
const merged = { ...obj, c: 3 };     // { a:1, b:2, c:3 }

// Function arguments
function sum(a, b, c) { return a + b + c; }
sum(...[1, 2, 3]); // 6
```

---

## Q16. What is the rest operator?

**Answer:**
The rest operator (`...`) collects multiple remaining elements/properties into a single array or object. It looks identical to spread but behaves oppositely — it *gathers* instead of *expanding*.

```javascript
// Function parameters
function sum(...nums) {
  return nums.reduce((acc, n) => acc + n, 0);
}
sum(1, 2, 3, 4); // 10

// Array destructuring
const [first, ...rest] = [1, 2, 3, 4];
console.log(first, rest); // 1 [2,3,4]

// Object destructuring
const { name, ...others } = { name: "Shohag", age: 24, city: "Khulna" };
console.log(name, others); // Shohag { age: 24, city: "Khulna" }
```

> **Interview Tip:** Spread vs rest depends on context — on the *right* side of `=` or in function calls it's spread (expanding); on the *left* side (destructuring/parameters) it's rest (collecting).

---

## Q17. What is the difference between shallow copy and deep copy?

**Answer:**

| Type | Description | Nested Objects |
|------|-------------|-----------------|
| **Shallow Copy** | Copies only the top-level properties; nested objects are still referenced (shared) | ❌ Not independent |
| **Deep Copy** | Recursively copies all levels; fully independent from the original | ✅ Independent |

```javascript
const original = { name: "Shohag", address: { city: "Khulna" } };

// Shallow copy
const shallow = { ...original };
shallow.address.city = "Dhaka";
console.log(original.address.city); // "Dhaka" — original changed too!

// Deep copy
const deep = structuredClone(original);
deep.address.city = "Chattogram";
console.log(original.address.city); // "Dhaka" — original NOT affected
```

---

## Q18. How do you clone an object?

**Answer:**

```javascript
const obj = { name: "Shohag", address: { city: "Khulna" } };

// 1. Spread operator - shallow copy
const clone1 = { ...obj };

// 2. Object.assign() - shallow copy
const clone2 = Object.assign({}, obj);

// 3. JSON methods - deep copy (but loses functions, undefined, Dates become strings)
const clone3 = JSON.parse(JSON.stringify(obj));

// 4. structuredClone() - true deep copy (modern, preferred)
const clone4 = structuredClone(obj);
```

| Method | Depth | Notes |
|--------|-------|-------|
| Spread `{...obj}` | Shallow | Fast, simple |
| `Object.assign()` | Shallow | Same as spread |
| `JSON.parse(JSON.stringify())` | Deep | Loses `undefined`, functions, `Symbol`, `Date` → string |
| `structuredClone()` | Deep | Modern, handles most data types correctly |

---

## Q19. How do you iterate over object properties?

**Answer:**
```javascript
const user = { name: "Shohag", age: 24, profession: "Developer" };

// for...in loop
for (const key in user) {
  console.log(key, user[key]);
}

// Object.keys() + forEach
Object.keys(user).forEach(key => {
  console.log(key, user[key]);
});

// Object.entries() + for...of (most common in modern code)
for (const [key, value] of Object.entries(user)) {
  console.log(key, value);
}
```

> **Interview Tip:** `for...in` also iterates inherited enumerable properties (from the prototype chain), so it's often safer to use `Object.keys()`/`Object.entries()`, which only include the object's own properties.

---

## Q20. What are `Object.keys()`, `Object.values()`, and `Object.entries()`?

**Answer:**

| Method | Returns |
|--------|---------|
| `Object.keys()` | Array of property names |
| `Object.values()` | Array of property values |
| `Object.entries()` | Array of `[key, value]` pairs |

```javascript
const user = { name: "Shohag", age: 24 };

Object.keys(user);    // ["name", "age"]
Object.values(user);  // ["Shohag", 24]
Object.entries(user); // [["name","Shohag"], ["age",24]]

// Rebuilding an object from entries
const entries = Object.entries(user);
const rebuilt = Object.fromEntries(entries); // { name:"Shohag", age:24 }
```

---

## Q21. What is optional chaining (`?.`)?

**Answer:**
Optional chaining safely accesses deeply nested properties without throwing an error if an intermediate property is `null` or `undefined` — it short-circuits and returns `undefined` instead.

```javascript
const user = { name: "Shohag", address: { city: "Khulna" } };

console.log(user.address?.city);   // "Khulna"
console.log(user.contact?.phone);  // undefined (no error, "contact" doesn't exist)

// Without optional chaining, this would throw:
// console.log(user.contact.phone); // ❌ TypeError

// Works with function calls too
user.greet?.(); // does nothing if greet doesn't exist, instead of throwing

// Works with array access
const arr = null;
console.log(arr?.[0]); // undefined
```

---

## Q22. What is the nullish coalescing operator (`??`)?

**Answer:**
`??` returns the right-hand value only if the left-hand value is `null` or `undefined` — unlike `||`, which also triggers on any falsy value (`0`, `""`, `false`, `NaN`).

```javascript
const count = 0;

console.log(count || 10); // 10 ❌ (0 is falsy, so || triggers)
console.log(count ?? 10); // 0  ✅ (0 is not null/undefined, so ?? keeps it)

let userInput = null;
console.log(userInput ?? "default"); // "default"

let name = "";
console.log(name ?? "Guest"); // "" (empty string is not nullish)
console.log(name || "Guest"); // "Guest"
```

> **Interview Tip:** Use `??` when `0`, `""`, or `false` are valid values you want to preserve — a common bug source with `||` in form/config defaults.

---

## Q23. What is `Object.freeze()`?

**Answer:**
`Object.freeze()` makes an object **immutable** — you cannot add, remove, or modify its properties (shallow freeze only).

```javascript
const user = Object.freeze({ name: "Shohag", age: 24 });

user.age = 30;        // fails silently (throws in strict mode)
delete user.name;     // fails silently
user.city = "Khulna"; // fails silently

console.log(user); // { name: "Shohag", age: 24 } — unchanged

console.log(Object.isFrozen(user)); // true
```

> **Interview Tip:** `Object.freeze()` is shallow — nested objects inside a frozen object are still mutable unless frozen separately (recursively).

```javascript
const obj = Object.freeze({ address: { city: "Khulna" } });
obj.address.city = "Dhaka"; // ✅ this works! nested object isn't frozen
```

---

## Q24. What is `Object.seal()`?

**Answer:**
`Object.seal()` prevents adding or removing properties, but **existing properties can still be modified** (unlike `freeze()`).

```javascript
const user = Object.seal({ name: "Shohag", age: 24 });

user.age = 30;        // ✅ works - can modify existing properties
user.city = "Khulna"; // ❌ fails - can't add new properties
delete user.name;     // ❌ fails - can't delete properties

console.log(user); // { name: "Shohag", age: 30 }
console.log(Object.isSealed(user)); // true
```

**Comparison:**

| Feature | `Object.freeze()` | `Object.seal()` |
|---------|---------------------|-------------------|
| Add properties | ❌ | ❌ |
| Delete properties | ❌ | ❌ |
| Modify existing properties | ❌ | ✅ |

---

## Q25. How do you check if a property exists in an object?

**Answer:**
```javascript
const user = { name: "Shohag", age: 24, city: undefined };

// 1. "in" operator - checks own AND inherited properties
console.log("name" in user); // true
console.log("city" in user); // true (even though value is undefined)

// 2. hasOwnProperty() - checks only own properties (not inherited)
console.log(user.hasOwnProperty("name")); // true

// 3. Object.hasOwn() - modern, recommended alternative to hasOwnProperty()
console.log(Object.hasOwn(user, "name")); // true

// 4. Checking value !== undefined (unreliable if property value IS undefined)
console.log(user.age !== undefined); // true
console.log(user.city !== undefined); // false, even though "city" key exists!
```

> **Interview Tip:** Prefer `in` or `Object.hasOwn()` over checking `!== undefined`, since a property can genuinely exist with a value of `undefined`.

---

# 💼 Common Interview Follow-up Questions

### 1. What is the difference between `Map` and `Object`?

| Feature | `Map` | `Object` |
|---------|-------|----------|
| Key types | Any type (objects, functions, etc.) | Strings/Symbols only |
| Key order | Guaranteed insertion order | Mostly insertion order (with integer-key exceptions) |
| Size | `.size` property | Manual (`Object.keys(obj).length`) |
| Iteration | Directly iterable (`for...of`) | Needs `Object.keys()/entries()` |
| Performance | Better for frequent add/remove | Better for static structures |

```javascript
const map = new Map();
map.set("name", "Shohag");
map.set(1, "one");
console.log(map.get("name")); // Shohag
console.log(map.size); // 2
```

### 2. What is the difference between `Set` and `Array`?

| Feature | `Set` | `Array` |
|---------|-------|---------|
| Duplicate values | Not allowed (auto-unique) | Allowed |
| Access by index | ❌ No | ✅ Yes |
| Built-in uniqueness | ✅ Yes | ❌ No |
| Order | Insertion order | Index order |

```javascript
const set = new Set([1, 2, 2, 3]);
console.log(set); // Set(3) {1, 2, 3}
console.log([...set]); // [1, 2, 3]
```

### 3. How does `reduce()` work internally?

`reduce()` iterates through the array, carrying an **accumulator** forward on each call and passing it to the next iteration.

```javascript
const nums = [1, 2, 3, 4];

const sum = nums.reduce((acc, curr, index, arr) => {
  console.log({ acc, curr, index });
  return acc + curr;
}, 0);

// Iteration 1: acc=0, curr=1 → returns 1
// Iteration 2: acc=1, curr=2 → returns 3
// Iteration 3: acc=3, curr=3 → returns 6
// Iteration 4: acc=6, curr=4 → returns 10
console.log(sum); // 10
```
If no initial value is provided, the first array element is used as the initial accumulator and iteration starts from the second element.

### 4. When should you use `map()` instead of `forEach()`?

- Use `map()` when you need a **new transformed array** as a result (chainable, functional).
- Use `forEach()` when you only need **side effects** (logging, DOM updates, API calls) and don't need a return value.

```javascript
// ✅ Good use of map() - building a new array
const doubled = [1,2,3].map(n => n * 2);

// ✅ Good use of forEach() - side effect only
[1,2,3].forEach(n => console.log(n));

// ❌ Bad: using map() just for side effects (wastes the returned array)
[1,2,3].map(n => console.log(n));
```

### 5. What is the time complexity of common array operations?

| Operation | Time Complexity | Reason |
|-----------|------------------|--------|
| Access by index (`arr[i]`) | O(1) | Direct memory offset |
| `push()` / `pop()` | O(1) | End of array, no re-indexing |
| `shift()` / `unshift()` | O(n) | All elements re-indexed |
| `splice()` (middle) | O(n) | Elements shifted |
| `indexOf()` / `includes()` | O(n) | Linear search |
| `find()` / `filter()` / `map()` | O(n) | Visits every element |
| `sort()` | O(n log n) | Comparison-based sort |

### 6. Explain reference types in JavaScript.

Objects, arrays, and functions are **reference types** — variables store a reference (memory address) to the value, not the value itself. Primitives (`string`, `number`, `boolean`, `null`, `undefined`, `symbol`, `bigint`) are **value types** and are copied by value.

```javascript
// Primitive - copied by value
let a = 10;
let b = a;
b = 20;
console.log(a); // 10 (unaffected)

// Reference type - copied by reference
let obj1 = { value: 10 };
let obj2 = obj1;
obj2.value = 20;
console.log(obj1.value); // 20 (both point to same object!)
```

### 7. How do you perform a deep clone of an object?

```javascript
const original = { name: "Shohag", address: { city: "Khulna" } };

// Best modern approach
const clone = structuredClone(original);

// Older approach (has limitations with functions, undefined, Dates)
const clone2 = JSON.parse(JSON.stringify(original));

// Manual recursive deep clone (for understanding, or custom needs)
function deepClone(obj) {
  if (obj === null || typeof obj !== "object") return obj;
  if (Array.isArray(obj)) return obj.map(deepClone);
  return Object.fromEntries(
    Object.entries(obj).map(([key, value]) => [key, deepClone(value)])
  );
}
```

### 8. What are computed property names?

Computed property names let you use an expression (in `[]`) as an object's key, evaluated dynamically.

```javascript
const key = "profession";
const value = "Developer";

const user = {
  name: "Shohag",
  [key]: value,          // computed key
  [`is${key}`]: true,    // "isprofession": true
};
console.log(user); // { name: "Shohag", profession: "Developer", isprofession: true }
```

### 9. What are object property descriptors?

Every object property has an internal descriptor controlling its behavior: `value`, `writable`, `enumerable`, and `configurable`.

```javascript
const user = { name: "Shohag" };

console.log(Object.getOwnPropertyDescriptor(user, "name"));
// { value: "Shohag", writable: true, enumerable: true, configurable: true }

// Customizing a property
Object.defineProperty(user, "age", {
  value: 24,
  writable: false,   // can't be reassigned
  enumerable: false, // won't show in for...in / Object.keys()
  configurable: false, // can't be deleted or redefined
});

user.age = 30;
console.log(user.age); // 24 (write blocked)
console.log(Object.keys(user)); // ["name"] (age is hidden)
```

### 10. Explain immutable updates in JavaScript.

Immutable updates create a **new** object/array instead of mutating the original — essential in frameworks like React for correct re-rendering and predictable state.

```javascript
// Object - immutable update
const user = { name: "Sk Shohag", age: 24 };
const updatedUser = { ...user, age: 25 }; // new object, original untouched

// Array - immutable update
const nums = [1, 2, 3];
const addedNum = [...nums, 4];              // add
const removedNum = nums.filter(n => n !== 2); // remove
const updatedNum = nums.map(n => n === 2 ? 20 : n); // update

console.log(nums); // [1,2,3] — original unchanged
```

> **Interview Tip:** In React, mutating state directly (e.g., `state.push(x)`) won't trigger a re-render because the reference doesn't change. Always create new objects/arrays for state updates.

---
