# Advanced JavaScript Interview Questions

---

# ⚡ Optimizing Large Array Operations

## ❓ How do you optimize large array operations (`map/filter/reduce`) for performance?

### ✅ Optimization Techniques
- Avoid multiple iterations when possible
- Combine operations into a single loop
- Use `for` loops for heavy computations
- Avoid unnecessary object creation
- Use memoization/caching
- Process large datasets in chunks

---

## ❌ Less Efficient

```javascript
const result = arr
  .filter(x => x > 10)
  .map(x => x * 2);
```

This iterates through the array multiple times.

---

## ✅ More Optimized

```javascript
const result = [];

for (let i = 0; i < arr.length; i++) {
  if (arr[i] > 10) {
    result.push(arr[i] * 2);
  }
}
```

Uses a single loop for better performance.

---

# ⏱️ Debouncing vs Throttling

## ❓ Explain debouncing & throttling — when do you use which?

| Debouncing | Throttling |
|---|---|
| Delays execution until action stops | Executes at fixed intervals |
| Prevents unnecessary calls | Limits repeated execution |
| Best for search inputs | Best for scroll/resize |

---

## ✅ Debouncing Use Cases
- Search bars
- Auto-save forms
- API calls while typing

### Example

```javascript
searchInput.addEventListener("input", debounce(search, 500));
```

---

## ✅ Throttling Use Cases
- Infinite scrolling
- Window resizing
- Mouse movement tracking

### Example

```javascript
window.addEventListener("scroll", throttle(loadData, 300));
```

---

# ⚖️ Loose vs Strict Equality

## ❓ How do loose & tight equality impact performance?

| Loose Equality (`==`) | Strict Equality (`===`) |
|---|---|
| Performs type coercion | No type conversion |
| Slightly slower | Faster & predictable |
| Can cause unexpected bugs | Recommended approach |

---

## ✅ Example

```javascript
0 == false   // true
0 === false  // false
```

### ✅ Best Practice
Always prefer:

```javascript
===
```

for safer and cleaner comparisons.

---

# 🐞 Debugging Complex Async Code

## ❓ What’s your approach to debugging complex async code?

### ✅ Common Strategies
- Use `async/await`
- Add proper `try/catch`
- Use detailed logging
- Debug promise chains carefully
- Monitor API/network requests
- Use browser DevTools

---

## ✅ Example

```javascript
async function fetchData() {
  try {
    const response = await fetch("/api/data");
    const data = await response.json();

    console.log(data);

  } catch (error) {
    console.error(error);
  }
}
```

---

# 📡 Custom Event Emitter

## ❓ How would you write a custom event emitter?

### ✅ Basic Implementation

```javascript
class EventEmitter {

  constructor() {
    this.events = {};
  }

  on(event, callback) {
    if (!this.events[event]) {
      this.events[event] = [];
    }

    this.events[event].push(callback);
  }

  emit(event, data) {
    if (this.events[event]) {
      this.events[event].forEach(cb => cb(data));
    }
  }
}

const emitter = new EventEmitter();

emitter.on("message", data => {
  console.log(data);
});

emitter.emit("message", "Hello");
```

---

## ✅ Real-Time Use Cases
- Chat systems
- Notifications
- Pub/Sub architecture
- Component communication

---

# 🧠 Deep Cloning with JSON.parse(JSON.stringify())

## ❓ What happens when you deep clone using `JSON.parse(JSON.stringify())`?

### ✅ Advantages
- Simple deep cloning method
- Easy for basic objects

---

## ❌ Limitations

It removes:
- Functions
- `undefined`
- `Date` objects
- `Map`
- `Set`
- Circular references

---

## ✅ Example

```javascript
const obj = {
  date: new Date()
};

const clone = JSON.parse(JSON.stringify(obj));

console.log(typeof clone.date);
```

### Output

```javascript
string
```

`Date` becomes a string after cloning.

---

## ✅ Better Alternative

Use:

```javascript
structuredClone()
```

for modern deep cloning support.

---

---

# 🎨 CSS

## ❓ Difference Between Inline and Block Elements

| Inline Elements | Block Elements |
|---|---|
| Occupies only required width | Occupies full available width |
| Doesn't start on a new line | Starts on a new line |
| Width and height usually don't apply | Width and height can be controlled |

### ✅ Inline Examples

```html
<span>Hello</span>
<a href="#">Link</a>
<strong>Text</strong>
```

### ✅ Block Examples

```html
<div>Content</div>
<p>Paragraph</p>
<section>Section</section>
```

---

## ❓ What is CSS Isolation?

CSS Isolation means limiting styles to a specific component or scope so they don't affect other components.

### ✅ Methods
- CSS Modules
- Shadow DOM
- Styled Components
- Tailwind CSS
- CSS-in-JS Libraries

### ✅ Benefits
- Prevents style conflicts
- Easier maintenance
- Better component reusability

---

## ❓ Adaptive vs Responsive Web Design

| Adaptive Design | Responsive Design |
|---|---|
| Multiple fixed layouts | Flexible layout |
| Device-specific designs | Fluid design |
| More maintenance | Easier maintenance |
| Uses predefined breakpoints | Uses flexible grids |

### ✅ Adaptive Example
Different layouts for:
- Mobile
- Tablet
- Desktop

### ✅ Responsive Example
Uses:
- Flexbox
- CSS Grid
- Media Queries

to automatically adjust content.

---

## ❓ What is Tailwind CSS and Why is it Famous?

Tailwind CSS is a utility-first CSS framework that provides pre-built utility classes.

### ✅ Example

```html
<button class="bg-blue-500 text-white p-2 rounded">
  Submit
</button>
```

### ✅ Why It Is Popular
- Faster development
- No need to write large CSS files
- Consistent UI design
- Easy customization
- Smaller production builds

### ✅ Benefits
- Rapid prototyping
- Reusable utility classes
- Better maintainability

---

## ❓ What is the Purpose of Garbage Collection?

Garbage Collection automatically removes unused objects from memory.

### ✅ Benefits
- Prevents memory leaks
- Frees unused memory
- Improves application performance

### ✅ JavaScript Uses
- Mark-and-Sweep Algorithm

---

## ❓ How to Convert a Callback Function into a Promise?

### Callback Version

```javascript
function getData(callback) {
  setTimeout(() => {
    callback("Data Loaded");
  }, 1000);
}
```

### Promise Version

```javascript
function getData() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      resolve("Data Loaded");
    }, 1000);
  });
}
```

---

## ❓ What Happens When You Await a Non-Promise Value?

JavaScript automatically wraps the value using:

```javascript
Promise.resolve(value)
```

### Example

```javascript
async function demo() {
  const result = await 100;

  console.log(result);
}
```

### Output

```javascript
100
```

---

## ❓ What is TypeScript?

TypeScript is a superset of JavaScript that adds static typing.

### ✅ Features
- Type Safety
- Interfaces
- Generics
- Better Tooling
- Compile-Time Error Detection

### ✅ Benefits
- Easier maintenance
- Better scalability
- Fewer runtime errors

---

## ❓ Why Do We Use Generic Functions?

Generics allow functions to work with multiple data types while maintaining type safety.

### Example

```typescript
function identity<T>(value: T): T {
  return value;
}
```

### ✅ Benefits
- Reusability
- Type safety
- Cleaner code

---

## ❓ How Will You Handle Security in APIs?

### ✅ Security Practices

- JWT Authentication
- OAuth
- HTTPS
- Input Validation
- Rate Limiting
- CORS Protection
- SQL Injection Prevention
- XSS Protection

### ✅ Additional Measures

- Secure Cookies
- Access Control
- Refresh Tokens

---

## ❓ Error Handling in REST APIs

### Best Practices

- Use proper HTTP status codes
- Return meaningful error messages
- Centralized error handling
- Logging and monitoring

### Example

```json
{
  "status": 404,
  "message": "User not found"
}
```

---

## ❓ What is API Versioning?

API Versioning helps maintain backward compatibility when APIs evolve.

### Common Approaches

```text
/api/v1/users
/api/v2/users
```

### Benefits
- Safe upgrades
- Backward compatibility
- Easier maintenance

---

## ❓ How Will You Monitor and Debug API Latency?

### Monitoring Techniques

- API response time logging
- Database query monitoring
- Load testing
- Application Performance Monitoring (APM)

### Tools

- Postman
- New Relic
- Datadog
- Grafana
- Chrome DevTools

### Debugging Process

1. Identify slow API endpoints
2. Analyze network requests
3. Inspect database queries
4. Check server logs
5. Optimize bottlenecks

---
---

# 8️⃣ Difference Between `null` and `undefined`

| null | undefined |
|--------|------------|
| Intentional absence of value | Variable declared but not assigned |
| Assigned by developer | Assigned by JavaScript |
| Type is object (historical bug) | Type is undefined |

### Example

```javascript
let a = null;
let b;

console.log(a); // null
console.log(b); // undefined
```

### Use Cases

#### null
```javascript
const user = null;
```

Represents intentionally empty value.

#### undefined

```javascript
let age;
```

Variable exists but no value assigned.

---

# 9️⃣ What is a Closure?

A closure is a function that remembers variables from its outer scope even after the outer function has finished execution.

### Example

```javascript
function counter() {

  let count = 0;

  return function() {
    count++;
    return count;
  };
}

const increment = counter();

console.log(increment());
console.log(increment());
console.log(increment());
```

### Output

```javascript
1
2
3
```

### Real-World Uses

- Data hiding
- Event handlers
- Memoization
- Timers

---

# 🔟 What is the Event Loop?

The Event Loop allows JavaScript to handle asynchronous operations even though JavaScript is single-threaded.

### Flow

```text
Call Stack
     ↓
Web APIs
     ↓
Callback Queue
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

### Output

```javascript
Start
End
Timeout
```

### Why?

`setTimeout` callback goes to the callback queue and executes only when the call stack becomes empty.

---

# 1️⃣1️⃣ Return Unique Values From Array

### Using Set (Recommended)

```javascript
function getUnique(arr) {
  return [...new Set(arr)];
}

console.log(
  getUnique([1,2,2,3,3,4])
);
```

### Output

```javascript
[1,2,3,4]
```

### Complexity

```text
Time: O(n)
Space: O(n)
```

---

# 1️⃣2️⃣ Difference Between bind(), call(), and apply()

All three methods are used to change the value of `this`.

### call()

Invokes immediately and accepts arguments individually.

```javascript
function greet(city) {
  console.log(this.name, city);
}

const person = {
  name: "Hari"
};

greet.call(person, "Hyderabad");
```

---

### apply()

Invokes immediately and accepts arguments as an array.

```javascript
greet.apply(person, ["Hyderabad"]);
```

---

### bind()

Returns a new function.

```javascript
const newFn =
  greet.bind(person, "Hyderabad");

newFn();
```

---

### Summary

| Method | Invokes Immediately | Arguments |
|----------|------------------|------------|
| call | ✅ | Individual |
| apply | ✅ | Array |
| bind | ❌ | Returns function |

---

# 1️⃣3️⃣ What is a Promise?

A Promise represents the eventual completion or failure of an asynchronous operation.

### States

```text
Pending
Fulfilled
Rejected
```

### Example

```javascript
const promise = new Promise(
  (resolve, reject) => {

    setTimeout(() => {
      resolve("Success");
    }, 1000);

  }
);

promise.then((data) => {
  console.log(data);
});
```

### Output after 1 second

```javascript
Success
```

---

# 1️⃣4️⃣ Deep Clone vs Shallow Clone

## Shallow Copy

Copies only the first level.

```javascript
const obj = {
  name: "Hari",
  address: {
    city: "Hyderabad"
  }
};

const copy = {...obj};
```

### Problem

```javascript
copy.address.city = "Chennai";

console.log(obj.address.city);
```

Output:

```javascript
Chennai
```

---

## Deep Copy

Creates completely independent copies.

### Using structuredClone()

```javascript
const deepCopy =
  structuredClone(obj);
```

---

### Custom Deep Clone

```javascript
function deepClone(obj) {

  if (
    obj === null ||
    typeof obj !== "object"
  ) {
    return obj;
  }

  let clone =
    Array.isArray(obj)
      ? []
      : {};

  for (let key in obj) {
    clone[key] =
      deepClone(obj[key]);
  }

  return clone;
}
```

### Difference

| Shallow Copy | Deep Copy |
|--------------|-----------|
| First level only | Entire object |
| Shares nested references | Independent copy |
| Faster | More expensive |

---

# 1️⃣5️⃣ What is Debouncing?

Debouncing delays function execution until the user stops triggering the event for a specified time.

### Common Uses

- Search bars
- API requests
- Auto-save forms

### Example

```javascript
function debounce(fn, delay) {

  let timer;

  return function(...args) {

    clearTimeout(timer);

    timer = setTimeout(() => {
      fn(...args);
    }, delay);

  };
}
```

### Usage

```javascript
const search =
  debounce(() => {
    console.log("Searching...");
  }, 500);
```

---

## 8. Closures in JavaScript

A closure allows a function to access variables from its outer scope even after the outer function has finished execution.

### Example

```javascript
function counter() {
  let count = 0;

  return function() {
    count++;
    return count;
  };
}

const increment = counter();
```

### Real-World Uses
- Data privacy
- Event handlers
- Timers
- Memoization

---

## 9. JavaScript Event Loop

JavaScript is single-threaded.

### Flow
1. Call Stack executes synchronous code
2. Async tasks move to Web APIs
3. Completed tasks move to Callback Queue
4. Event Loop pushes them back to Call Stack

### Purpose
Enables asynchronous non-blocking behavior.

---

## 10. Event Delegation

Instead of attaching events to multiple child elements, a single event listener is attached to the parent element using event bubbling.

### Benefits
- Better performance
- Less memory usage
- Handles dynamically added elements

---

---

## 1. Explain Closure with a Real Use Case

A closure is created when a function remembers variables from its outer scope even after the outer function has finished executing.

### Example

```javascript
function createCounter() {
  let count = 0;

  return function () {
    count++;
    return count;
  };
}

const counter = createCounter();

console.log(counter());
console.log(counter());
console.log(counter());
```

### Output

```javascript
1
2
3
```

### Real-World Use Cases

- Data privacy
- Authentication state
- Memoization
- Event handlers
- Timers

### Example: User Session

```javascript
function createSession() {
  let token = "abc123";

  return {
    getToken() {
      return token;
    }
  };
}
```

---

## 2. How Does the Event Loop Work in Async API Calls?

JavaScript is single-threaded but can handle asynchronous operations using the Event Loop.

### Flow

```text
Call Stack
↓
Web APIs
↓
Callback Queue
↓
Event Loop
↓
Call Stack
```

### Example

```javascript
console.log("Start");

fetch("/users")
  .then(() => {
    console.log("Data Loaded");
  });

console.log("End");
```

### Output

```javascript
Start
End
Data Loaded
```

The API request runs outside the call stack and executes after the stack becomes empty.

---

## 3. Difference Between Microtasks and Macrotasks

### Microtasks

- Promise callbacks
- queueMicrotask()
- MutationObserver

### Macrotasks

- setTimeout
- setInterval
- DOM Events

### Example

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

### Output

```javascript
Start
End
Promise
Timeout
```

### Why?

Microtasks always execute before Macrotasks.

---

## 4. How Does Debouncing Help in Search APIs?

Debouncing delays function execution until the user stops typing.

### Without Debouncing

```text
H → API Call
Ha → API Call
Har → API Call
Hari → API Call
```

### With Debouncing

```text
User Stops Typing
↓
One API Call
```

### Example

```javascript
function debounce(fn, delay) {
  let timer;

  return (...args) => {
    clearTimeout(timer);

    timer = setTimeout(() => {
      fn(...args);
    }, delay);
  };
}
```

### Benefits

- Reduces API requests
- Improves performance
- Saves server resources

---

## 5. What Causes Memory Leaks in JavaScript?

### Common Reasons

#### Unremoved Event Listeners

```javascript
window.addEventListener("resize", handler);
```

#### Unclosed Timers

```javascript
setInterval(() => {}, 1000);
```

#### Closures Holding References

```javascript
function outer() {
  const hugeData = new Array(1000000);

  return () => hugeData;
}
```

#### Detached DOM Nodes

References remain after DOM removal.

### Prevention

- Remove listeners
- Clear timers
- Clean useEffect
- Avoid unnecessary references

---



##  What are Higher-Order Functions?

A Higher-Order Function is a function that:

- Accepts another function as an argument, or
- Returns a function

### Examples

```javascript
const numbers = [1, 2, 3, 4];

const doubled = numbers.map((num) => num * 2);
```

### Custom Example

```javascript
function greet(callback) {
  callback();
}

greet(() => console.log("Hello"));
```

---

##  What are Pure Functions?

A Pure Function:

- Produces the same output for the same input.
- Has no side effects.

### Pure Function

```javascript
function add(a, b) {
  return a + b;
}
```

### Impure Function

```javascript
let count = 0;

function increment() {
  count++;
}
```

Reason: Modifies external state.

---

##  Difference Between var, let, and const

| Feature    | var      | let       | const     |
| ---------- | -------- | --------- | --------- |
| Scope      | Function | Block     | Block     |
| Redeclare  | Yes      | No        | No        |
| Reassign   | Yes      | Yes       | No        |
| Hoisting   | Yes      | Yes       | Yes       |
| TDZ        | No       | Yes       | Yes       |

### Example

```javascript
{
  var a = 10;
  let b = 20;
}

console.log(a); // 10
console.log(b); // ReferenceError
```

---

##  Output-Based Question (var vs let)

### Code

```javascript
for (var i = 0; i < 5; i++) {
  setTimeout(function () {
    console.log("var:", i);
  }, 1000);
}

for (let i = 0; i < 5; i++) {
  setTimeout(function () {
    console.log("let:", i);
  }, 1000);
}
```

### Output

```text
var: 5
var: 5
var: 5
var: 5
var: 5

let: 0
let: 1
let: 2
let: 3
let: 4
```

### Reason

#### var

`var` is function-scoped.

All callbacks share the same variable `i`.

By the time `setTimeout` executes:

```javascript
i === 5
```

#### let

`let` is block-scoped.

A new `i` is created for every iteration.

---

### Fixing var Using Closure

```javascript
for (var i = 0; i < 5; i++) {
  ((i) => {
    setTimeout(() => {
      console.log(i);
    }, 1000);
  })(i);
}
```

Output:

```text
0
1
2
3
4
```

---

## What are Promises in JavaScript?

A Promise represents the eventual completion (or failure) of an asynchronous operation.

### States

```text
Pending
   ↓
Fulfilled
or
Rejected
```

### Example

```javascript
const promise = new Promise((resolve, reject) => {
  resolve("Success");
});

promise.then((result) => console.log(result));
```

Output:

```text
Success
```

---

## Promise.all() vs Promise.any()

### Promise.all()

Waits for all promises to resolve.

```javascript
Promise.all([
  fetchUsers(),
  fetchPosts(),
  fetchComments(),
]);
```

### Behavior

- Resolves when all succeed.
- Rejects immediately if one fails.

### Use Case

Dashboard where all APIs are required.

---

### Promise.any()

Returns the first successfully resolved promise.

```javascript
Promise.any([
  apiServer1(),
  apiServer2(),
  apiServer3(),
]);
```

### Behavior

- Resolves when one succeeds.
- Rejects only if all fail.

### Use Case

Multiple mirror servers or CDN endpoints.

---

### Comparison

| Promise.all() | Promise.any() |
|--------------|--------------|
| All must succeed | One success is enough |
| Fails on first rejection | Fails only if all reject |
| Returns all results | Returns first successful result |

---
