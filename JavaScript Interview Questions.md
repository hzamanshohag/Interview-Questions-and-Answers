# JavaScript Interview Questions

# Core JavaScript Concepts

## 1. JavaScript Introduction

<aside>
📌 **Topic: What is JavaScript?**

</aside>

A **high-level**, **interpreted programming language** called JavaScript makes creating interactive web pages and online apps with dynamic functionality possible. Commonly called the universal language, developers primarily use JavaScript for front-end and back-end work.

---

<aside>
📌 **Topic: Who created JavaScript?**

</aside>

JavaScript was created by **Brendan Eich** in **1995** during his time at Netscape Communications. Initially, it was developed under the name **`Mocha`**, but later the language was officially called **`LiveScript`** when it first shipped in beta releases of Netscape.

---

<aside>
📌 **Topic: What is the V8 JavaScript engine?**

</aside>

V8 is an **open-source high-performance** JavaScript engine used by the **Google Chrome browser**, written in **`C++`**. It is also being used in the node.js project. It implements ECMAScript and Web Assembly and runs on Windows 7 or later, macOS 10.12+, and Linux systems that use x64, IA-32, ARM, or MIPS processors. 

---

<aside>
📌 **Topic: Why is JavaScript treated as Single threaded?**

</aside>

JavaScript is a **single-threaded language**. Because the language specification does not allow the programmer to write code so that the interpreter can run parts of it in parallel in multiple threads or processes. Whereas languages like Java, go, and C++ can make multi-threaded and multi-process programs.

---

<aside>
📌 **Topic: Why use Node.js for backend with JavaScript?**

</aside>

- **Single Language**: Node.js allows full-stack development using JavaScript, meaning you can use the same language on both the client-side and server-side.
- **Asynchronous, Non-blocking I/O:** Node.js employs an event-driven, non-blocking I/O model, enabling it to handle multiple requests concurrently with high efficiency.
- **Large Ecosystem**: The npm (Node Package Manager) ecosystem offers numerous libraries, making development faster and easier.
- **Community Support**: With a large developer community, Node.js is constantly evolving with robust libraries and frameworks.
- **Other Backend Options**: While you could use Python (Django, Flask) or Ruby (Rails), they typically don't offer the same non-blocking I/O advantages or seamless integration with front-end JavaScript.

---

<aside>
📌 **Topic: What is Strict Mode in JavaScript?**

</aside>

**Strict mode** is a feature in JavaScript that helps developers write safer and cleaner code by enforcing stricter parsing and error handling. It eliminates silent errors and disallows certain actions like:

- Using undeclared variables.
- Assigning to read-only properties.
- Deleting variables, etc.

---

## **2. Data Types and Variables**

<aside>
📌 **Topic: What are the different data types in JavaScript?**

</aside>

- JavaScript has **six** primitive data types:
    1. Number
    2. String
    3. Boolean
    4. Null
    5. Undefined
    6. Symbol
- It also has **two** compound data types:
    1. Object
    2. Array

---

<aside>
📌 **Topic: What is the difference between null and undefined?**

</aside>

**`null` ****is an assignment value that represents no value or an **empty** value, while **`undefined`** is a variable that has been **declared but not assigned** a value.

Below are the main differences between null and undefined:

| Null | Undefined |
| --- | --- |
| It is an assignment value which indicates that variable points to no object. | It is not an assignment value where a variable has been declared but has not yet been assigned a value. |
| Type of null is object | Type of undefined is undefined |
| The null value is a primitive value that represents the null, empty, or non-existent reference. | The undefined value is a primitive value used when a variable has not been assigned a value. |
| Indicates the absence of a value for a variable | Indicates absence of variable itself |
| Converted to zero (0) while performing primitive operations | Converted to NaN while performing primitive operations |

---

<aside>
📌 **Topic: What is the difference between “var” and “let” keywords in JavaScript?**

</aside>

The **`var`** keyword declares a **global variable**, which means that the variable can be accessed from anywhere in the code. The **`let`** keyword declares a **local variable**, which means that the variable can only be accessed within the **block of code** where it is declared.

| var | let |
| --- | --- |
| It has been available from the beginning of JavaScript | Introduced as part of ES6 |
| It has **function scope** | It has **block scope** |
| Variable declaration will be **hoisted**, **initialized as undefined** | **Hoisted but not initialized** |
| It is possible to re-declare the variable in the same scope | It is not possible to re-declare the variable |

---

<aside>
📌 **Topic: What is the difference between “let”, “const”, and “var”?**

</aside>

**`let`** and **`const`** were introduced in ES6 and have **block scope**. **`let`** is **re-assignable**, and **`const`** is **non re-assignable**. **`var`** is **function-scoped** and can **be redeclared** and **reassigned** throughout the function.

---

## **3. Syntax and Operators**

<aside>
📌 **Topic: What is the difference between == and === operators in JavaScript?**

</aside>

The equality `==` operator is a comparison operator that **compares two values** and returns true if they are equal. The strict equality `===` operator is also a comparison operator, but it **compares two values** and returns true only if they are equal and of the **same type**.

Some of the example which covers the above cases:

```jsx
0 == false   // true
0 === false  // false
1 == "1"     // true
1 === "1"    // false
null == undefined // true
null === undefined // false
'0' == false // true
'0' === false // false
NaN == NaN or NaN === NaN // false
[]==[] or []===[] //false, refer different objects in memory
{}=={} or {}==={} //false, refer different objects in memory
```

---

## **4. Functions and Scope**

<aside>
📌 **Topic: What is a first-class and first-order function in JavaScript?**

</aside>

In JavaScript, **functions are first-class objects**. First-class functions mean when functions in that language are treated like any other variable.

```jsx
const handler = () => console.log("This is a click handler function");
document.addEventListener("click", handler);
```

A first-order function is a function that **doesn’t accept another function as an argument** and doesn’t return a function as its return value.

```jsx
const firstOrder = () => console.log("I am a first order function!");
```

---

<aside>
📌 **Topic: What is the scope in JavaScript?**

</aside>

**Scope is the accessibility of variables**, **functions**, and **objects** in some particular part of your code during runtime. In other words, scope determines the visibility of variables and other resources in areas of your code.

---

<aside>
📌 **Topic: What is hoisting in JavaScript?**

</aside>

Hoisting is a JavaScript mechanism where **variables**, **functions**, and **classes** are **moved to the top of their scope before code execution**. This means that variables and functions can be used before they are declared, as long as they are declared before they are used in a function.

**Function** Declarations Are Fully Hoisted. **`let`** and **`const`** are hoisted,, BUT in a **Temporal Dead Zone (TDZ).** A **temporal dead zone (TDZ)** is the area of a block where a variable is inaccessible until the moment the computer completely initializes it with a value. The **Temporal Dead Zone (TDZ)** refers to the time between when a variable is **hoisted** and when it is **initialized** in memory. During this period, accessing the variable will throw a **`ReferenceError`**.

```tsx
console.log(a); // ❌ ReferenceError: Cannot access 'a' before initialization
let a = 10;

// Engine sets up the environment:
// TDZ starts here
// a is hoisted (known to engine), BUT not initialized
TDZ starts for 'a'
let a; // declared, but in TDZ

// TDZ ends when 'a' is initialized
a = 10;
```

---

<aside>
📌 **Topic: What are higher-order functions in JavaScript?**

</aside>

A higher-order function is a function that **accepts another function as an argument** or **returns a function as a return value**, or both. The syntactic structure of the higher-order function will be as follows:

```jsx
const firstOrderFunc = () =>
  console.log("Hello, I am a first-order function");
  
const higherOrder = (ReturnFirstOrderFunc) => ReturnFirstOrderFunc();
higherOrder(firstOrderFunc);
```

---

<aside>
📌 **Topic: What is a unary function in JavaScript?**

</aside>

A unary function (i.e. monadic) is a function that **accepts exactly one argument**. It stands for a single argument accepted by a function. Let us take an example of unary function:

```jsx
const unaryFunction = (a) => console.log(a + 10); 
// Add 10 to the given argument and display the value
```

---

<aside>
📌 **Topic: What is the currying function in JavaScript?**

</aside>

Currying is the process of **taking a function with multiple arguments and turning it into a sequence of functions** each with only a single argument. Currying is named after the mathematician Haskell Curry. By applying currying, an n-ary function turns into a unary function. Let's take an example of n-ary function and how it turns into a currying function:

```jsx
const multiArgFunction = (a, b, c) => a + b + c;
console.log(multiArgFunction(1, 2, 3)); // 6

const curryUnaryFunction = (a) => (b) => (c) => a + b + c;
curryUnaryFunction(1); // returns a function: b => c =>  1 + b + c
curryUnaryFunction(1)(2); // returns a function: c => 3 + c
curryUnaryFunction(1)(2)(3); // returns the number 6
```

---

<aside>
📌 **Topic: What is a pure function in JavaScript?**

</aside>

In JavaScript, a pure function is a function that always **produces the same output for the same input** and **has no side effects**. It does not depend on any state or data change during a program’s execution. Rather, it only depends on its input arguments.

```jsx
const add = (x, y) => x + y;

add(2, 4); // Output: 6
```

---

<aside>
📌 **Topic: What is an anonymous function in JavaScript?**

</aside>

An anonymous function is a **function without a name**! Anonymous functions are commonly assigned to a variable name or used as a callback function.

```jsx
function (optionalParameters) {
  //do something
}

const myFunction = function(){ //Anonymous function assigned to a variable
  //do something
};

[1, 2, 3].map(function(element){ //Anonymous function used as a callback function
  //do something
});
```

---

<aside>
📌 **Topic: What is Function Composition?**

</aside>

It is an approach where the **result of one function is passed on to the next function**, which is passed to another until the final function is executed for the final result.

```jsx
const double = (x) => x * 2;
const square = (x) => x * x;

var output1 = double(2);
var output2 = square(output1);
console.log(output2);

var output_final = square(double(2));
console.log(output_final);
```

---

<aside>
📌 **Topic: What is JavaScript Scope, and define Block Scope, Global Scope, and Lexical Scope?**

</aside>

**Scope** in JavaScript determines the **visibility** and **accessibility** of variables and functions in different parts of the code.

- **Global Scope**: Variables defined outside any function or block have **global scope** and are accessible throughout the code.
- **Block Scope**: Variables declared inside **`{}`** (with **`let`** or **`const`**) have **block scope** and are only accessible within that block.
- **Lexical Scope**: Refers to how functions can access variables from the **outer scopes** in which they are defined, even after those outer scopes have returned. This allows for **closure** in JavaScript.

---

<aside>
📌 **Topic: What is Lexical Scope?**

</aside>

Lexical scope is the **ability for a function scope to access variables from the parent scope**. This consists of the variable environment and the reference to the outer environment (parent scope). Each execution context has its own lexical environment.

```jsx
function outerFunction() {
  var outerVariable = 'I am from outerFunction';

  function innerFunction() {
    var innerVariable = 'I am from innerFunction';
    console.log(outerVariable); // Accessible
  }

  innerFunction();
  console.log(innerVariable); // Not accessible (ReferenceError)
}

outerFunction();
```

---

<aside>
📌 **Topic: What are closures in JavaScript?**

</aside>

A **closure** is a feature in JavaScript where an **inner function has access** to the variables of its **outer function** even **after the outer function has finished executing**.

A closure is the **combination of a function bundled together** (enclosed) with references to its surrounding state (the lexical environment). i.e, It is an inner function that has access to the outer or enclosing function’s variables, functions and other data even after the outer function has finished its execution. The closure has three scope chains.

1. Own scope where variables defined between its curly brackets
2. Outer function's variables
3. Global variables

```jsx
function Welcome(name) {
  var greetingInfo = function (message) {
    console.log(message + " " + name);
  };
  return greetingInfo;
}
var myFunction = Welcome("John");
myFunction("Welcome "); //Output: Welcome John
myFunction("Hello Mr."); //output: Hello Mr. John
```

---

<aside>
📌 **Topic: What is the difference between `map` and `forEach` functions?**

</aside>

- Both **`map`** and **`forEach`** functions are used to iterate over an arrays but there are some differences in their functionality.
    1. **Returning values:** The **`map`** method **returns a new array** with transformed elements whereas **`forEach`** method returns **`undefined`** even though both of them are doing the same job.
        
        ```jsx
          const arr = [1, 2, 3, 4, 5];
          arr.map(x => x * x); // [1, 4, 9, 16, 25]
          arr.forEach(x => x * x); //
        
        // The `forEach()` method in JavaScript always returns undefined. This is because forEach() is used to iterate over arrays and perform side effects on each element, rather than returning a `new array or transforming the original array`
        ```
        
    2. **Chaining methods:** The **`map`** method is **chainable**. i.e, It can be attached with **`reduce`**, **`filter`**, **`sort`** and other methods as well. Whereas **`forEach`** cannot be attached with any other methods because it returns **`undefined`** value.
        
        ```jsx
          const arr = [1, 2, 3, 4, 5];
          arr.map(x => x * x).reduce((total, cur) => total + cur); // 55
          arr.forEach(x => x * x).reduce((total, cur) => total + cur); 
        // Uncaught TypeError: Cannot read properties of undefine(reading 'reduce')
        ```
        
    3. **Mutation:** The **`map`** method **doesn't mutate the original array** by returning new array. Whereas **`forEach`** method also doesn't mutate the original array but it's callback is allowed to mutate the original array.

---

<aside>
📌 **Topic: What is the difference between Call by Value and Call by Reference in JavaScript?**

</aside>

- **Call by Value**: Primitive data types (like numbers, strings) are passed by value, meaning a **copy** of the variable is passed to the function, and changes inside the function do not affect the original variable.
    
    ```jsx
    let a = 5;
    function modify(x) {
      x = 10;
    }
    modify(a);
    console.log(a); 
    // 5 (unchanged)
    ```
    
- **Call by Reference**: Objects and arrays are passed by reference, meaning the **actual reference** to the memory location is passed, and changes to the object or array within the function will reflect in the original variable.
    
    ```jsx
    let obj = { name: 'John' };
    function modify(o) {
      o.name = 'Alice';
    }
    modify(obj);
    console.log(obj.name); 
    // "Alice"
    ```
    

---

<aside>
📌 **Topic: Difference Between Shallow Copy and Deep Copy in JavaScript?**

</aside>

- **Shallow Copy**: A shallow copy copies the references of objects and arrays, meaning nested objects are still referenced from the original. Changes in the nested structure of the copy will affect the original.
    
    ```jsx
    let original = { name: "John", address: { city: "New York" } };
    let shallowCopy = { ...original };
    shallowCopy.address.city = "Los Angeles";  
    // Also changes original.address.city
    ```
    
- **Deep Copy**: A deep copy creates a completely independent copy of an object, including nested objects, so changes in the copy won't affect the original.
    
    ```jsx
    let deepCopy = JSON.parse(JSON.stringify(original));
    ```
    

---

## **5. Control Flow (Loops, Conditionals)**

<aside>
📌 **Topic: What is the purpose of switch-case?**

</aside>

The switch case statement in JavaScript is used for **decision-making purposes**. In a few cases, using the switch case statement is going to be more convenient than if-else statements

```jsx
switch (expression)
{
    case value1:
        statement1;
        break;
    case value2:
        statement2;
        break;
    .
    .
    case valueN:
        statementN;
        break;
    default:
        statementDefault;
}
```

---

<aside>
📌 **Topic: What is for...in statement?**

</aside>

The **`for...in`** statement **iterates over all enumerable string properties of an object**, including inherited enumerable properties.

```jsx
const object = { a: 1, b: 2, c: 3 };

for (const property in object) {
  console.log(`${property}: ${object[property]}`); // "a: 1" "b: 2" "c: 3"
}
```

---

<aside>
📌 **Topic: What is for...of statement?**

</aside>

The for...of statement creates a loop **iterating over iterable objects or elements** such as built-in String, Array, Array-like objects (like arguments or NodeList), TypedArray, Map, Set, and user-defined iterables.

```jsx
let array = [10, 20, 30, 40, 50];

for (let value of array) {
  value++;
  console.log(value); // 11 21 31 41 51
}
```

---

<aside>
📌 **Topic: What are the differences between for...of and for...in statements?**

</aside>

- Both for...in and for...of statements iterate over JavaScript data structures. The only difference is over what they iterate:
    1. **for…in iterates over all enumerable property keys of an object**
    2. **for…of iterates over the values of an iterable object.**
- Since for..in loop iterates over the keys of the object, the first loop logs 0, 1, 2 and newProp while iterating over the array object. The for...of loop iterates over the values of a arr data structure and logs a, b, c in the console.

```jsx
let arr = ["a", "b", "c"];

arr.newProp = "newVlue";

// key are the property keys
for (let key in arr) {
  console.log(key); // 0, 1, 2 & newProp
}

// value are the property values
for (let value of arr) {
  console.log(value); // a, b, c
}
```

---

## 6. JavaScript Methods

<aside>
📌 **Topic: Explain the difference between `call`, `bind`, and `apply` in JavaScript?**

</aside>

- **Call**: The **`call()`** method is used to invoke a function with a specific **`this`** value and arguments passed individually. It allows you to define the context (i.e., the object) for a function and execute it immediately.
    
    ```jsx
    function greet() {
      console.log(`Hello, ${this.name}`);
    }
    const person = { name: 'Alice' };
    greet.call(person); 
    // Output: "Hello, Alice"
    ```
    
- **Apply**: The **`apply()`** method works similarly to **`call()`**, but the arguments are passed as an array. This is useful when you have an array of data you want to use as arguments.
    
    ```jsx
    greet.apply(person, []); 
    // Output: "Hello, Alice"
    ```
    
- **Bind**: The **`bind()`** method returns a **new function** with a bound **`this`** value and any preset arguments. Unlike **`call`** or **`apply`**, the function is not invoked immediately but can be called later.
    
    ```jsx
    const boundGreet = greet.bind(person);
    boundGreet(); 
    // Output: "Hello, Alice"
    ```
    

---

<aside>
📌 **Topic: What is the purpose of the array slice method?**

</aside>

The **`slice()`** method **returns the selected elements** in an array as a new array object. It selects the elements starting at the given start argument, and ends at the given optional end argument without including the last element. If you omit the second argument then it selects till the end of the array. This method can also accept a negative index which counts back from the end of the array.

```jsx
let arrayIntegers = [1, 2, 3, 4, 5];
let arrayIntegers1 = arrayIntegers.slice(0, 2); // returns [1,2]
let arrayIntegers2 = arrayIntegers.slice(2, 3); // returns [3]
let arrayIntegers3 = arrayIntegers.slice(4); //returns [5]
let arrayIntegers4 = arrayIntegers.slice(-3, -1); //returns [3, 4]
```

---

<aside>
📌 **Topic: What is the purpose of the array splice method?**

</aside>

The **`splice()`** method **adds/removes items to/from an array**, and then returns the removed item. The first argument specifies the array position/index for insertion or deletion whereas the optional second argument indicates the number of elements to be deleted. Each additional argument is added to the array.

```jsx
let arrayIntegersOriginal1 = [1, 2, 3, 4, 5];
let arrayIntegersOriginal2 = [1, 2, 3, 4, 5];
let arrayIntegersOriginal3 = [1, 2, 3, 4, 5];

let arrayIntegers1 = arrayIntegersOriginal1.splice(0, 2); // returns [1, 2]; original array: [3, 4, 5]
let arrayIntegers2 = arrayIntegersOriginal2.splice(3); // returns [4, 5]; original array: [1, 2, 3]
let arrayIntegers3 = arrayIntegersOriginal3.splice(3, 1, "a", "b", "c"); //returns [4]; original array: [1, 2, 3, "a", "b", "c", 5]
```

---

<aside>
📌 **Topic: What is the difference between slice and splice?**

</aside>

| Slice | Splice |
| --- | --- |
| **Doesn't modify the original array(immutable)** | **Modifies the original array(mutable)** |
| Returns the subset of original array | Returns the deleted elements as array |
| Used to pick the elements from array | Used to insert/delete elements to/from array |

---

<aside>
📌 **Topic: What is the use of `setTimeout`?**

</aside>

The **`setTimeout()`** method is used to **call a function or evaluate an expression after a specified number of milliseconds**.

```jsx
setTimeout(function () {
  console.log("Hello World!");
}, 2000);
```

---

<aside>
📌 **Topic: What is the use of `setInterval`?**

</aside>

The **`setInterval()`** method is used to **call a function or evaluate an expression at specified intervals in milliseconds**.

```jsx
setInterval(function () {
  console.log("Hello World!");
}, 2000);
```

---

<aside>
📌 **Topic: What is the purpose of some method in arrays?**

</aside>

The **`some()`** method is used to test whether at least one element in the array passes the test implemented by the provided function. The method returns a boolean value.

```jsx
var array = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

var odd = (element) => element % 2 !== 0;

console.log(array.some(odd)); // true (the odd element exists)
```

---

<aside>
📌 **Topic: Explain the `reduce()` method in JavaScript. Can you provide some examples of how it's used?**

</aside>

The **`reduce()`** method in JavaScript is a powerful array method used to **reduce an array to a single value**. It applies a function to each element of the array (from left to right), passing the result of the previous function call as an argument to the next one. This process continues until the array has been completely traversed, resulting in a single accumulated value.

- **Syntax:**

```jsx
array.reduce(callback(accumulator, currentValue, currentIndex, array), initialValue);
```

- **`callback`**: The function to execute on each element in the array.
    - **`accumulator`**: The accumulated value from the previous iteration (or the **`initialValue`** for the first iteration).
    - **`currentValue`**: The current element being processed in the array.
    - **`currentIndex`** (optional): The index of the current element.
    - **`array`** (optional): The array **`reduce`** was called upon.
- **`initialValue`** (optional): A value to use as the first argument to the first call of the callback. If no **`initialValue`** is supplied, the first element in the array will be used, and iteration will start from the second element.

```jsx
// Sum of All Elements in an Array
const numbers = [1, 2, 3, 4];
const sum = numbers.reduce((accumulator, currentValue) => accumulator + currentValue, 
0);
console.log(sum); // Output: 10
```

---

<aside>
📌 **Topic: What is the `this` keyword in JavaScript, and what is its purpose?**

</aside>

The **`this`** keyword in JavaScript refers to the **object that is executing the current function** Its value is determined by how the function is called:

- In the **global context**, **`this`** refers to the **global object** (**`window`** in browsers, **`global`** in Node.js).
- In the context of an **object method**, **`this`** refers to the **object itself**.
- In **event handlers**, **`this`** refers to the **DOM element** that the event is fired on.
- In **strict mode**, **`this`** remains **`undefined`** if it’s not explicitly set.
- In **constructor functions** or **classes**, **`this`** refers to the new instance being created.

---

<aside>
📌 **Topic: What is Method Chaining in JavaScript?**

</aside>

**Method chaining** in JavaScript is a technique that allows you to call multiple methods on the same object consecutively in a single line. Each method returns the object itself (using **`this`**), enabling the next method in the chain to be called.

```jsx
class Calculator {
  constructor(value = 0) {
    this.value = value;
  }

  add(num) { this.value += num; return this; }
  subtract(num) { this.value -= num; return this; }
  multiply(num) { this.value *= num; return this; }
  divide(num) { if (num !== 0) this.value /= num; return this; }

  result() { return this.value; }
}

const calc = new Calculator();
let finalResult = calc.add(10).subtract(3).multiply(2).divide(2).result();
console.log(finalResult);  
// Output: 7
```

---

<aside>
📌 **Topic: Describe the use of the `new` keyword in JavaScript?**

</aside>

The **`new`** keyword in JavaScript is used to create an instance of a constructor function. When used, it:

1. Creates a new object.
2. Sets the **`this`** keyword in the constructor to point to the new object.
3. Links the new object to the prototype of the constructor.
4. Returns the newly created object unless the constructor returns its own object.

---

# Advanced JavaScript

## **1. Asynchronous Programming (Callbacks, Promises, Async/Await)**

<aside>
📌 **Topic: What is a Callback Function in JavaScript?**

</aside>

A callback function is a function **passed into another function as an argument**, which is then **invoked inside the outer function to complete an action**. The callbacks are needed because JavaScript is an event-driven language. That means instead of waiting for a response javascript will keep executing while listening for other events.

```jsx
function callbackFunction(name) {
  console.log("Hello " + name);
}

function outerFunction(callback) {
  let name = prompt("Please enter your name.");
  callback(name);
}

outerFunction(callbackFunction);
```

---

<aside>
📌 **Topic: What is a Promise in JavaScript?**

</aside>

A Promise is **an object representing the eventual completion or failure of an asynchronous operation**.  Promises are used to handle asynchronous operations. They provide an alternative approach for callbacks by reducing the callback hell and writing cleaner code.

- Promises have **three states**:
    1. **Pending:** This is an initial state of the Promise before an operation begins
    2. **Fulfilled:** This state indicates that the specified operation was completed.
    3. **Rejected:** This state indicates that the operation was not complete. In this case, an error value will be thrown.

The action flow of a promise will be as below:

![Untitled](Untitled.png)

```jsx
const promise = new Promise(
  (resolve) => {
    setTimeout(() => {
      resolve("I'm a Promise!");
    }, 5000);
  },
  (reject) => {}
);

promise.then((value) => console.log(value));
```

---

<aside>
📌 **Topic: What is Promise Chaining and Promise All?**

</aside>

The process of executing a sequence of asynchronous tasks one after another using promises is known as Promise chaining.

```jsx
new Promise(function (resolve, reject) {
  setTimeout(() => resolve(1), 1000);
})
  .then(function (result) {
    console.log(result); // 1
    return result * 2;
  })
  .then(function (result) {
    console.log(result); // 2
    return result * 3;
  })
  .then(function (result) {
    console.log(result); // 6
    return result * 4;
  });
```

**`Promise.all`** is a promise that takes an array of promises as an input (an iterable), and it gets resolved when all the promises get resolved or any one of them gets rejected.

```jsx
Promise.all([Promise1, Promise2, Promise3]) .then(result) => {   console.log(result) }) .catch(error => console.log(`Error in promises ${error}`))
```

---

<aside>
📌 **Topic: What is an Async function in JavaScript?**

</aside>

An async function is a function declared with the **`async`** keyword which enables asynchronous, promise-based behavior to be written in a cleaner style by avoiding promise chains. These functions can contain zero or more **`await`** expressions.

```jsx
async function logger() {
  let data = await fetch("http://someapi.com/users"); // pause until fetch returns
  console.log(data);
}
logger();
```

---

<aside>
📌 **Topic: What is the difference between a callback function and the `return` statement in JavaScript?**

</aside>

- **Callback Function**: A callback is a function passed as an argument to another function, which is executed once the parent function has completed. Callbacks are typically used in **asynchronous** code where operations (e.g., fetching data from an API) might take time, and you don’t want to block the execution of other code.
    
    ```jsx
    function fetchData(callback) {
      setTimeout(() => {
        callback('Data fetched');
      }, 1000);
    }
    fetchData(data => console.log(data)); 
    // Output: "Data fetched" after 1 second
    ```
    
- **Return Statement**: The **`return`** statement **exits a function** and optionally returns a value. Unlike callbacks, **`return`** is **synchronous** and halts further execution in the function once it is reached.
    
    ```jsx
    function sum(a, b) {
      return a + b;
    }
    const result = sum(3, 4); 
    // result = 7
    ```
    

---

## **2. Event Loop and Concurrency Model**

<aside>
📌 **Topic: What is heap in JavaScript?**

</aside>

Heap memory in JavaScript is a region in the **computer's memory** used for **dynamic memory allocation.** This is where JavaScript **stores non-primitive data** types, such as **objects**, **arrays**, and **functions**. i.e., values that are **reference types**. This is the place where all the memory allocations and de-allocation take place. Both heap and call-stack are two containers of JS runtime. Whenever runtime comes across variables and function declarations in the code it stores them in the Heap.

![Untitled](Untitled%201.png)

---

<aside>
📌 **Topic: What is event loop in JavaScript?**

</aside>

JavaScript’s event loop is the core mechanism that enables **asynchronous operations**. Though single-threaded, it manages tasks efficiently. Imagine it as a queue system: events like user interactions or network requests are added to the queue, and the engine processes them one by one. This allows JavaScript to handle non-blocking tasks without freezing, keeping the application responsive even while waiting for data or other operations.

- Workflow of event loop:
    1. **Call Stack:** JavaScript uses a call stack to keep track of the currently executing function (where the program is in its execution).
    2. **Callback Queue:** Asynchronous operations, such as I/O operations or timers, are handled by the browser or Node.js runtime. When these operations are complete, corresponding functions (callbacks) are placed in the callback queue.
    3. **Event Loop:** The event loop continuously checks the call stack and the callback queue. If the call stack is empty, it takes the first function from the callback queue and pushes it onto the call stack for execution.
    4. **Execution:** The function on top of the call stack is executed. If this function contains asynchronous code, it might initiate further asynchronous operations.
    5. **Callback Execution:** When an asynchronous operation is complete, its callback is placed in the callback queue.
    6. **Repeat:** The event loop continues this process, ensuring that the call stack is always empty before taking the next function from the callback queue.

![Untitled](Untitled%202.png)

---

<aside>
📌 **Topic: What is Event Bubbling in JavaScript?**

</aside>

Event bubbling is a **type of event propagation** where the event **first triggers on the innermost target element**, and then successively **triggers on the ancestors (parents) of the target element** in the same nesting hierarchy till it reaches the outermost DOM element(i.e, global window object).

```jsx
<body>
    <h2>Bubbling Event in Javascript</h2>
    <div id="parent">
        <button>
            <h2>Parent</h2>
        </button>
        <button id="child">
            <p>Child</p>
        </button>
    </div>
    <br>
    <script>
        document.getElementById(
        "child").addEventListener("click", function () {
            alert("You clicked the Child element!");
        });
        
        document.getElementById(
        "parent").addEventListener("click", function () {
            alert("You clicked the parent element!");
        });
    </script>
</body>
// Child
// Parent
```

---

<aside>
📌 **Topic: What is Event Capturing in JavaScript?**

</aside>

Event capturing is a **type of event propagation** where the event is **first captured by the outermost element**, and then **successively triggers on the descendants (children) of the target element** in the same nesting hierarchy till it reaches the innermost target DOM element.

You need to pass **`true`** value for **`addEventListener`** method to trigger event handlers in event capturing phase.

```jsx
<body>
    <h2>Bubbling Event in Javascript</h2>
    <div id="parent">
        <button>
            <h2>Parent</h2>
        </button>
        <button id="child">
            <p>Child</p>
        </button>
    </div>
    <br>
    <script>
        document.getElementById(
        "child").addEventListener("click", function () {
            alert("You clicked the Child element!");
        }, true);
        
        document.getElementById(
        "parent").addEventListener("click", function () {
            alert("You clicked the parent element!");
        });
    </script>
</body>
// Parent
// Child
```

---

<aside>
📌 **Topic: What is Event Delegation in JavaScript?**

</aside>

Event delegation is a technique for **listening to events where you delegate a parent element** as the listener for all of the events that happen inside it.

```jsx
 <script>
  // Listen for changes to fields inside the form
	document.getElementById(
  "form").addEventListener(
  "input",
  function (event) {
    // Log the field that was changed
    console.log(event.target);
	  },
	  false
	);
</script>
```

---

<aside>
📌 **Topic: What is the `stopPropagation` and `preventDefault` method in JavaScript?**

</aside>

The **`stopPropagation`** method is used to stop the event from bubbling up the event chain.

```jsx
<p>Click DIV1 Element</p>
<div onclick="secondFunc()">DIV 2
  <div onclick="firstFunc(event)">DIV 1</div>
</div>

<script>
function firstFunc(event) {
  alert("DIV 1");
  event.stopPropagation();
}

function secondFunc() {
  alert("DIV 2");
}
</script>
```

The **`preventDefault`** method cancels the event if it is cancelable, meaning that the default action or behaviour that belongs to the event will not occur.

```jsx
document
  .getElementById("link")
  .addEventListener("click", function (event) {
    event.preventDefault();
  });
```

---

<aside>
📌 **Topic: Difference between Cluster and Child Process Models?**

</aside>

- **Cluster Model**: Used to scale applications by forking multiple worker processes, each running on a separate core of the CPU. The workers share the same server port.
- **Child Process Model**: Involves creating child processes to perform tasks separately from the main process. These processes have their own memory space and do not share the same port.

---

## **3. Memory Management and Garbage Collection**

## **4. Recursion and Memoization**

<aside>
📌 **Topic: What is a function in JavaScript, and what is a recursive function?**

</aside>

- **Function**: A function is a block of code designed to perform a specific task. It can be called multiple times, potentially with different arguments, to produce different outputs.
    
    ```jsx
    function greet(name) {
      return `Hello, ${name}`;
    }
    ```
    
- **Recursive Function**: A recursive function is a function that **calls itself** within its body. It is used to solve problems that can be broken down into smaller, similar problems.
    
    ```jsx
    function factorial(n) {
      if (n <= 1) return 1;
      return n * factorial(n - 1);
    }
    ```
    

---

<aside>
📌 **Topic: What is memoization in JavaScript?**

</aside>

**Memoization** is an optimization technique used to speed up functions by **caching** the results of expensive function calls and returning the cached result when the same inputs occur again.
Memoization is a technique that can be used to improve the performance of JavaScript code. Memoization works by storing the results of expensive calculations in a cache. This allows the JavaScript code to avoid re-performing the expensive calculations if the same input is provided again.

```jsx
function factorial(n) {
	if (n === 0) {
		return 1
	}
	else {
	return n * factorial(n - 1);
	}
}
```

---

# **Modern JavaScript (ES6 and Beyond)**

## 1. Introduction of ES6

<aside>
📌 **Topic: What is ECMAScript?**

</aside>

ECMAScript is the scripting language that forms the basis of JavaScript. ECMAScript standardized by the ECMA International standards organization in the ECMA-262 and ECMA-402 specifications. The first edition of ECMAScript was released in 1997.

---

<aside>
📌 **Topic: What is ES6?**

</aside>

ES6 is the sixth edition of the javascript language and it was released in June 2015. It was initially known as ECMAScript 6 (ES6) and later renamed to ECMAScript 2015. Almost all the modern browsers support ES6 but for the old browsers there are many transpilers, like Babel.js etc.

---

<aside>
📌 **Topic: List down some of the features of ES6?**

</aside>

- Below are the list of some new features of ES6:
    1. Support for constants or immutable variables
    2. Block-scope support for variables, constants and functions
    3. Arrow functions
    4. Default parameters
    5. Rest and Spread Parameters
    6. Template Literals
    7. Multi-line Strings
    8. Destructuring Assignment
    9. Enhanced Object Literals
    10. Promises
    11. Classes
    12. Modules

---

## **2. Syntax Enhancements**

<aside>
📌 **Topic: What is a spread operator?**

</aside>

Spread operator allows iterables ( arrays / objects / strings ) to be expanded into single arguments/elements.

```jsx
// function argments
const numbers = [1, 2, 3, 4];
function add(a, b, c, d) {
  return a + b + c + d;
}

console.log(add(...numbers)); // Output: 10

// array literals
// copying an array
const originalArray = [1, 2, 3];
const copiedArray = [...originalArray];

console.log(copiedArray); // Output: [1, 2, 3]

// concatenating an array
const array1 = [1, 2];
const array2 = [3, 4];
const combinedArray = [...array1, ...array2];

console.log(combinedArray); // Output: [1, 2, 3, 4]

// object literals
// copying an object
const originalObject = { a: 1, b: 2 };
const copiedObject = { ...originalObject };

console.log(copiedObject); // Output: { a: 1, b: 2 }

// merging an object
const object1 = { a: 1 };
const object2 = { b: 2 };
const mergedObject = { ...object1, ...object2 };

console.log(mergedObject); // Output: { a: 1, b: 2 }
```

---

<aside>
📌 **Topic: What is a rest parameter?**

</aside>

Rest parameter is an improved way to handle function parameters which allows us to represent an indefinite number of arguments as an array.

```jsx
function greet(greeting, ...names) {
  return `${greeting}, ${names.join(' and ')}!`;
}

console.log(greet('Hello', 'Alice', 'Bob', 'Charlie')); // Output: Hello, Alice and Bob and Charlie!
```

---

<aside>
📌 **Topic: What is an Unary operator?**

</aside>

The unary(+) operator is used to convert a variable to a number. If the variable cannot be converted, it will still become a number but with the value NaN.

```jsx
var x = "100";
var y = +x;
console.log(typeof x, typeof y); // string, number

var a = "Hello";
var b = +a;
console.log(typeof a, typeof b, b); // string, number, NaN
```

---

<aside>
📌 **Topic: What are template literals?**

</aside>

Template literals or template strings are string literals allowing embedded expressions. These are enclosed by the back-tick (`) character instead of double or single quotes. 

```jsx
var greeting = `Welcome to JS World, Mr. ${firstName} ${lastName}.`;
```

---

<aside>
📌 **Topic: What are nesting templates?**

</aside>

The nesting template is a feature supported within template literals syntax to allow inner backticks inside a placeholder ${ } within the template.

```jsx
const iconStyles = `icon ${
  isMobilePlatform()
    ? ""
    : `icon-${user.isAuthorized ? "submit" : "disabled"}`
}`;
```

---

<aside>
📌 **Topic: What is destructuring assignment?**

</aside>

The destructuring assignment is a JavaScript expression that makes it possible to unpack values from arrays or properties from objects into distinct variables.

```jsx
// array destructure
var [one, two, three] = ["JAN", "FEB", "MARCH"];

console.log(one); // "JAN"
console.log(two); // "FEB"
console.log(three); // "MARCH"

// object destructure
var { name, age } = { name: "John", age: 32 };

console.log(name); // John
console.log(age); // 32
```

---

<aside>
📌 **Topic: What are default values in destructuring assignment?**

</aside>

A variable can be assigned a default value when the value unpacked from the array or object is undefined during destructuring assignment. 

```jsx
// array default value
var x, y, z;

[x = 2, y = 4, z = 6] = [10];
console.log(x); // 10
console.log(y); // 4
console.log(z); // 6

// object default value
var { x = 2, y = 4, z = 6 } = { x: 10 };

console.log(x); // 10
console.log(y); // 4
console.log(z); // 6
```

---

<aside>
📌 **Topic: How do you swap variables in destructuring assignment?**

</aside>

If you don't use destructuring assignment, swapping two values requires a temporary variable. Whereas using a destructuring feature, two variable values can be swapped in one destructuring expression. 

```jsx
var x = 10,
  y = 20;

[x, y] = [y, x];
console.log(x); // 20
console.log(y); // 10
```

---

<aside>
📌 **Topic: What is nullish coalescing operator**

</aside>

It is a logical operator that returns its right-hand side operand when its left-hand side operand is null or undefined, and otherwise returns its left-hand side operand. This can be contrasted with the logical OR (||) operator, which returns the right-hand side operand if the left operand is any falsy value, not only null or undefined.

```jsx
console.log(null ?? true); // true
console.log(false ?? true); // false
console.log(undefined ?? true); // true
```

---

<aside>
📌 **Topic: What is optional chaining?**

</aside>

The optional chaining operator (?.) permits reading the value of a property located deep within a chain of connected objects without having to expressly validate that each reference in the chain is valid.

```jsx
const adventurer = {
  name: "Alice",
  cat: {
    name: "Dinah",
  },
};

const dogName = adventurer.dog?.name;
console.log(dogName);
// expected output: undefined

console.log(adventurer.someNonExistentMethod?.());
// expected output: undefined
```

---

## **3. Classes and Inheritance**

<aside>
📌 **Topic: What is a class in JavaScript, and how does it differ from a function?**

</aside>

A **class in JavaScript is a template for creating objects**. It encapsulates data and functions that operate on that data. Classes can contain constructors, methods, getters, setters, and static methods. While functions in JavaScript can also create objects (using constructor functions), classes provide a more structured and clear syntax for doing so, making the code easier to read and maintain.

---

<aside>
📌 **Topic: What are classes in ES6?**

</aside>

There are three concepts in Object-Oriented Programming **Object**, **Class,** and **Methods**. ES6 JavaScript supports Object-Oriented programming components.

- **Object:** A real-time object entity means the presentation of any entity in real-time.
- **Class:** It is the before the plan of creating any objects which is known as the blueprint of any objects which you want to create.
- **Methods:** It communicates between the objects.

The class contains the **Constructors** and **Functions**. The Constructors take responsibility for allocating memory for the objects of the class. The function takes responsibility of the action of the objects. Combing these two Constructor and **Functions** to make the **Class**.

```jsx
class Bike {
  constructor(color, model) {
    this.color = color;
    this.model = model;
  }

  getDetails() {
    return this.model + " bike has" + this.color + " color";
  }
}
```

---

<aside>
📌 **Topic: What is a class constructor in JavaScript, and how is it used?**

</aside>

A constructor in JavaScript is a special method of a class that is automatically called when a new instance of the class is created. It is used to initialize the object's properties and can also accept parameters to set those properties.

```jsx
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
}

const person1 = new Person('Alice', 30);
console.log(person1.name); // Output: Alice
console.log(person1.age);  // Output: 30
```

---

<aside>
📌 **Topic: How do you define methods in a JavaScript class?**

</aside>

Methods in a JavaScript class are defined as regular functions within the class body, but they are attached to the prototype of the class instances. These methods can be called on the class instances.

```jsx
class Animal {
  constructor(name) {
    this.name = name;
  }

  speak() {
    console.log(`${this.name} makes a noise.`);
  }
}

const dog = new Animal('Dog');
dog.speak(); // Output: Dog makes a noise.
```

---

<aside>
📌 **Topic: What is inheritance in JavaScript, and how is it implemented using classes?**

</aside>

Inheritance in JavaScript is a mechanism that allows one class to inherit properties and methods from another class. This is implemented using the **`extends`** keyword. The class that inherits is called the child (or subclass), and the class it inherits from is called the parent (or superclass).

```jsx
class Animal {
  constructor(name) {
    this.name = name;
  }

  speak() {
    console.log(`${this.name} makes a noise.`);
  }
}

class Dog extends Animal {
  speak() {
    console.log(`${this.name} barks.`);
  }
}

const dog = new Dog('Rex');
dog.speak(); // Output: Rex barks.
```

---

<aside>
📌 **Topic: What is the purpose of the `super` keyword in JavaScript classes?**

</aside>

The **`super`** keyword is used to call the constructor of the parent class and access its properties and methods. It is often used in derived classes to initialize properties from the base class.

```jsx
class Animal {
  constructor(name) {
    this.name = name;
  }

  speak() {
    console.log(`${this.name} makes a noise.`);
  }
}

class Dog extends Animal {
  constructor(name, breed) {
    super(name); // Calls the constructor of Animal
    this.breed = breed;
  }

  speak() {
    console.log(`${this.name} barks.`);
  }
}

const dog = new Dog('Buddy', 'Golden Retriever');
dog.speak(); // Output: Buddy barks.

```

---

<aside>
📌 **Topic: What are getters and setters in JavaScript classes, and how are they used?**

</aside>

Getters and setters are special methods that provide a way to access and modify the properties of an object. A getter method retrieves the value of a property, and a setter method sets the value of a property.

```jsx
class Person {
  constructor(name) {
    this._name = name; // Private property (by convention)
  }

  // Getter for the name property
  get name() {
    return this._name;
  }

  // Setter for the name property
  set name(newName) {
    if (newName && newName.length > 0) {
      this._name = newName;
    } else {
      console.log('Name must be a non-empty string.');
    }
  }
}

const person = new Person('Alice');

// Using the getter to access the name
console.log(person.name); // Output: Alice

// Using the setter to change the name
person.name = 'Bob';
console.log(person.name); // Output: Bob

// Trying to set an invalid name
person.name = ''; // Output: Name must be a non-empty string.
console.log(person.name); // Output: Bob
```

---

<aside>
📌 **Topic: What are modules?**

</aside>

Modules refer to small units of independent, reusable code and also act as the foundation of many JavaScript design patterns. Most of the JavaScript modules export an object literal, a function, or a constructor

---

<aside>
📌 **Topic: What is a prototype chain?**

</aside>

The prototype chain is a core JavaScript concept enabling the inheritance of properties and methods between objects. Every object has an internal link to another object called its **prototype**. This chain of links forms the **prototype chain**, which is used to **look up properties and methods**. It facilitates code reuse, efficient property lookup, and object hierarchy creation.

---

## **4. Iterators and Generators**

<aside>
📌 **Topic: What is an Iterator in JavaScript?**

</aside>

An iterator is an object that enables a programmer to traverse a collection, such as an array or an object, in a sequential manner without exposing the underlying structure of the collection. 

- In JavaScript, an iterator must implement a **`next()`** method that returns an object with two properties:
    1. **value**: The next value in the sequence.
    2. **done**: A boolean that indicates whether the iteration has completed (**`true`**) or if it can produce another value (**`false`**).

```jsx
function createIterator(array) {
  let index = 0;
  return {
    next: function() {
      if (index < array.length) {
        return { value: array[index++], done: false };
      } else {
        return { done: true };
      }
    }
  };
}

const iterator = createIterator(['a', 'b', 'c']);
console.log(iterator.next()); // { value: 'a', done: false }
console.log(iterator.next()); // { value: 'b', done: false }
console.log(iterator.next()); // { value: 'c', done: false }
console.log(iterator.next()); // { done: true }
```

---

<aside>
📌 **Topic: What is the `next()` method in the context of iterators?**

</aside>

The **`next()`** method is a fundamental part of the iterator protocol in JavaScript. It is used to advance through the elements of a collection or sequence, such as an array, object, or any iterable object.

- When called, the **`next()`** method returns an object containing two properties:
    1. **`value`**: The current value yielded by the iterator. This is the value of the next item in the sequence.
    2. **`done`**: A boolean indicating whether the iterator has completed its sequence. It is **`true`** when there are no more values to yield, and **`false`** otherwise.

```jsx
function createIterator(array) {
  let index = 0;

  return {
    next: function() {
      if (index < array.length) {
        return { value: array[index++], done: false };
      } else {
        return { value: undefined, done: true };
      }
    }
  };
}

const iterator = createIterator(['apple', 'banana', 'cherry']);
console.log(iterator.next()); // { value: 'apple', done: false }
console.log(iterator.next()); // { value: 'banana', done: false }
console.log(iterator.next()); // { value: 'cherry', done: false }
console.log(iterator.next()); // { value: undefined, done: true }
```

---

<aside>
📌 **Topic: What is an Generator in JavaScript?**

</aside>

A generator is a special type of function in JavaScript that can be paused and resumed during its execution. Generators are defined using the **`function*`** syntax and yield values to the caller using the **`yield`** keyword. Unlike regular functions that run to completion, generators maintain their state between executions and can produce multiple values over time.

```jsx
function* numberGenerator() {
  yield 1;
  yield 2;
  yield 3;
}

const gen = numberGenerator();
console.log(gen.next()); // { value: 1, done: false }
console.log(gen.next()); // { value: 2, done: false }
console.log(gen.next()); // { value: 3, done: false }
console.log(gen.next()); // { value: undefined, done: true }

```

---

<aside>
📌 **Topic: What are the methods used in generators function in JavaScript?**

</aside>

- Generators in JavaScript have a few specific methods that control their execution flow. Here are examples demonstrating the use of **`next()`**, **`return()`**, and **`throw()`** methods within a generator function:
    1. **`next()` Method:**
        
        The **`next()`** method is used to resume the generator's execution and advance to the next **`yield`** point. It returns an object containing **`value`** (the yielded value) and **`done`** (a boolean indicating if the generator is complete).
        
        ```jsx
        function* simpleGenerator() {
          yield 'First value';
          yield 'Second value';
          yield 'Third value';
        }
        
        const gen = simpleGenerator();
        
        console.log(gen.next()); // { value: 'First value', done: false }
        console.log(gen.next()); // { value: 'Second value', done: false }
        console.log(gen.next()); // { value: 'Third value', done: false }
        console.log(gen.next()); // { value: undefined, done: true }
        ```
        
    2. **`return()` Method**
        
        The **`return()`** method allows you to prematurely stop the generator's execution. It also returns an object similar to **`next()`**, with the **`done`** property set to **`true`**.
        
        ```jsx
        function* numberGenerator() {
          yield 1;
          yield 2;
          yield 3;
        }
        
        const gen = numberGenerator();
        
        console.log(gen.next());    // { value: 1, done: false }
        console.log(gen.return(42)); // { value: 42, done: true }
        console.log(gen.next());    // { value: undefined, done: true }
        ```
        
    3. **`throw()` Method:**
        
        The **`throw()`** method allows you to throw an error inside the generator, similar to throwing an exception in a regular function. This can be useful for handling errors or exceptions in the generator.
        
        ```jsx
        function* errorHandlingGenerator() {
          try {
            yield 1;
            yield 2;
            yield 3;
          } catch (e) {
            console.log('Error caught:', e);
          }
        }
        
        const gen = errorHandlingGenerator();
        
        console.log(gen.next());     // { value: 1, done: false }
        console.log(gen.next());     // { value: 2, done: false }
        console.log(gen.throw('An error occurred')); // Error caught: An error occurred
                                                    // { value: undefined, done: true }
        console.log(gen.next());     // { value: undefined, done: true }
        ```
        

---

# DOM and Browser APIs

## **1. DOM Manipulation and Event Handling**

<aside>
📌 **Topic: What is DOM?**

</aside>

HTML DOM (Document Object Model) is a **hierarchical representation of HTML documents**. It defines the structure and properties of elements on a webpage, enabling JavaScript to dynamically access, manipulate, and update content, enhancing interactivity and functionality.

---

<aside>
📌 **Topic: What is BOM?**

</aside>

The Browser Object Model (BOM) is a collection of objects exposed by the browser that allow JavaScript to interact with the browser window, document, and other browser-specific functionalities. The BOM includes objects such as **Window, Navigator, Location, History, and Screen**.

![Untitled](Untitled%203.png)

---

<aside>
📌 **Topic: What is the difference between window and document?**

</aside>

| Window | Document |
| --- | --- |
| It is the root level element in any web page | It is the direct child of the window object. This is also known as Document Object Model(DOM) |
| By default window object is available implicitly in the page | You can access it via **`window.document`** or document. |
| It has methods like alert(), confirm() and properties like document, location | It provides methods like **`getElementById`**, **`getElementsByTagName`**, **`createElement`,** etc |

---

## 2. Browser APIs

<aside>
📌 **Topic: What is a Cookie?**

</aside>

A cookie is a piece of data that is stored on your computer to be accessed by your browser. Cookies are saved as **key/value pairs**. 

- Cookies are used to remember information about the user profile (such as username). It basically involves two steps,
    1. When a user visits a web page, the user profile can be stored in a cookie.
    2. Next time the user visits the page, the cookie remembers the user profile.

![Untitled](Untitled%204.png)

| Attribute | Value Type | Purpose |
| --- | --- | --- |
| `name=value` | String | Stores the data |
| `Expires` | Date string | Expire cookie at a specific time |
| `Max-Age` | Number (seconds) | Set cookie lifespan from now |
| `Domain` | Domain name | Share cookie with subdomains |
| `Path` | URL path | Limit where cookie is sent |
| `Secure` | Flag | Send cookie only over HTTPS |
| `HttpOnly` | Flag | Prevent access via JavaScript |
| `SameSite` | `Strict`/`Lax`/`None` | Prevent CSRF and control cross-site behavior |

---

<aside>
📌 **Topic: What are the differences between cookie, local storage and session storage?**

</aside>

| Feature | Cookie | Local storage | Session storage |
| --- | --- | --- | --- |
| Accessed on client or server side | Both server-side & client-side | client-side only | client-side only |
| Lifetime | As configured using Expires option | until deleted | until tab is closed |
| SSL support | Supported | Not supported | Not supported |
| Maximum data size | 4KB | 5 MB | 5MB |

---

<aside>
📌 **Topic: What are the methods available on local and session storage?**

</aside>

```jsx
// Save data to localStorage or sessionStorage
localStorage.setItem("key", "value");
sessionStorage.setItem("key", "value");

// Get saved data from localStorage or sessionStorage
let data = localStorage.getItem("key");
let data = sessionStorage.getItem("key");

// Remove saved data from localStorage or sessionStorage
localStorage.removeItem("key");
sessionStorage.removeItem("key");

// Remove all saved data from localStorage or sessionStorage
localStorage.clear();
sessionStorage.clear();
```

---

<aside>
📌 **Topic: How do you access history in JavaScript?**

</aside>

The **`window.history`** object contains the browser's history. You can load previous and next URLs in the history using **`back()`** and **`next()`** methods.

```jsx
function goBack() {
  window.history.back();
}
function goForward() {
  window.history.forward();
}
```

---

<aside>
📌 **Topic: How do you redirect new page in JavaScript?**

</aside>

In JavaScript, you can redirect to a new page using the **`location`** property of window object.

```jsx
function redirect() {
  window.location.href = "newPage.html";
}
```

---

<aside>
📌 **Topic: How do you get the current url with JavaScript?**

</aside>

You can use **`window.location.href`** expression to get the current url path and you can use the same expression for updating the URL too.

```jsx
console.log("location.href", window.location.href); // Returns full URL
```

---

<aside>
📌 **Topic: What are the various url properties of location object?**

</aside>

- The below **`Location`** object properties can be used to access URL components of the page,
    1. href - The entire URL
    2. protocol - The protocol of the URL
    3. host - The hostname and port of the URL
    4. hostname - The hostname of the URL
    5. port - The port number in the URL
    6. pathname - The path name of the URL
    7. search - The query portion of the URL
    8. hash - The anchor portion of the URL

---

<aside>
📌 **Topic: How do get query string values in JavaScript?**

</aside>

You can use **`URLSearchParams`** to get query string values in JavaScript. 

```jsx
const urlParams = new URLSearchParams(window.location.search);
const clientCode = urlParams.get("clientCode");
```

---

## 3. Web APIs

<aside>
📌 **Topic: What is JSON?**

</aside>

JSON (JavaScript Object Notation) is a lightweight format that is used for data interchanging. It is based on a subset of JavaScript language in the way objects are built in JavaScript. easily be sent to and from a server, and used as a data format by any programming language.

---

<aside>
📌 **Topic: What is the purpose JSON `stringify` and `parse`?**

</aside>

When sending data to a web server, the data has to be in a string format. You can achieve this by converting JSON object into a string using **`stringify()`** method.

When receiving the data from a web server, the data is always in a string format. But you can convert this string value to a JavaScript object using **`parse(`**) method.

```jsx
// JSON stringify
var userJSON = { name: "John", age: 31 };
var userString = JSON.stringify(userJSON);
console.log(userString); //"{"name":"John","age":31}"

// JSON parse
var userString = '{"name":"John","age":31}';
var userJSON = JSON.parse(userString);
console.log(userJSON); // {name: "John", age: 31}
```

---

<aside>
📌 **Topic: What is same-origin policy?**

</aside>

The same-origin policy is a policy that prevents JavaScript from making requests across domain boundaries. An origin is defined as a combination of URI scheme, hostname, and port number. If you enable this policy then it prevents a malicious script on one page from obtaining access to sensitive data on another web page using Document Object Model(DOM).

---

# Notes

<aside>
📌 **Topic: What is api and rest api**

</aside>

. A REST API is a way for different software systems to talk to each other over the internet. It follows a set of rules that allow you to create, read, update, and delete data on a server using simple HTTP commands,

A REST API is an [application programming interface (API)](https://www.redhat.com/en/topics/api/what-are-application-programming-interfaces) that follows the design principles of the REST architectural style. REST is short for representational state transfer, and is a set of rules and guidelines about how you should build a web API.

When a client request is made via a RESTful API, it transfers a representation of the state of the resource to the requester or endpoint. This information, or representation, is delivered in one of several formats via HTTP: JSON (Javascript Object Notation), HTML, XLT, Python, PHP, or plain text. JSON is the most generally popular file format to use because, despite its name, it’s language-agnostic, as well as readable by both humans and machines.

---
