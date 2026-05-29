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
