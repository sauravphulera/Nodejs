# Episode 5: Diving into the Node.js GitHub Repository

## 🚀 Exploring How Modules Work Behind the Scenes

In this episode, we'll explore how **modules** actually work in Node.js. We’ll dive into how modules load into a page and how Node.js handles multiple modules, focusing on **module.exports** and **require()**.

---

## 🔹 Understanding Scope in JavaScript

```javascript
function x() {
  const a = 10;
  function b() {
    console.log("b");
  }
}
```

**Q: If you execute this code, will you be able to access `a` outside the function?**

**A:** No! The variable `a` is inside the function `x()`, making it inaccessible outside of it.

To learn more about scope, check out this video: [Understanding Scope in JavaScript](#).

---

## 🔹 How Modules Work in Node.js

Modules in Node.js work **similarly to function scopes**. When you `require()` a file, Node.js wraps the code inside a function, keeping all variables and functions private to the module unless explicitly exported.

```javascript
(function () {
  // All module code is wrapped inside this IIFE (Immediately Invoked Function Expression)
})();
```

### **Why Does Node.js Use IIFE?**

1. **Encapsulation** – Keeps variables and functions private to avoid conflicts.
2. **Immediate Execution** – Runs the code as soon as it's loaded.

---

## 🔹 How `require()` Works Behind the Scenes

1. **Resolving the Module Path** – Checks if the module is a local file, a JSON file, or in `node_modules`.
2. **Loading the Module** – Reads the content of the module file.
3. **Wrapping Inside an IIFE** – Encapsulates the module’s code.
4. **Evaluating and Exporting** – Runs the code and sets `module.exports`.
5. **Caching (Very Important!)** – Stores the module in memory for faster access in subsequent requires.

### **Example of Caching in Node.js**

```javascript
const xyz = require("./xyz"); // First time: Node.js loads and caches xyz module
const xyzAgain = require("./xyz"); // Second time: Node.js returns the cached module
```

Without caching, every `require()` call would reload and evaluate the module, affecting performance.

---

## 🔹 Where Does `module.exports` Come From?

When your module is wrapped inside a function, **Node.js provides an object called `module`**, which contains `module.exports`.

```javascript
console.log(module);
```

You can modify `module.exports` to expose specific functions or variables.

```javascript
module.exports = { greet: () => console.log("Hello World") };
```

---

## 🔹 Exploring Node.js Internals on GitHub

### **Key Files in Node.js Repository:**

- `require()` implementation: [node/lib/internal/modules/helpers.js](https://github.com/nodejs/node/blob/main/lib/internal/modules/helpers.js)
- `LazyModule()`: [node/lib/internal/modules/cjs/loader.js](https://github.com/nodejs/node/blob/main/lib/internal/modules/cjs/loader.js)
- `setTimeout` implementation: [node/lib/timers/promises.js](https://github.com/nodejs/node/blob/main/lib/timers/promises.js)

---

## 🔹 The Power of `libuv`

**Why is Node.js so popular?** 🚀 **Because of `libuv`!**

`libuv` provides:

- **Asynchronous I/O** handling
- **Event loop management**
- **Cross-platform compatibility**

Check out the **lib** folder in the Node.js GitHub repository to see built-in modules like `http`, `fs`, and `path` in action.

---

## 🔹 Where Does `setTimeout` Come From?

Did you know that `setTimeout` is not a part of JavaScript? It’s provided by the **Node.js runtime!**

🔗 [Check out its implementation in Node.js](https://github.com/nodejs/node/blob/main/lib/timers/promises.js)

---

## 📌 Summary

✅ **Modules in Node.js** are wrapped inside an **IIFE** for encapsulation.
✅ **`require()`** resolves, loads, wraps, evaluates, and caches modules.
✅ **`module.exports`** allows exporting functions and variables.
✅ **`libuv`** is the secret behind Node.js' **performance and scalability**.
✅ **`setTimeout`**, `fs`, and other APIs come from Node.js internals, not JavaScript itself.

💡 **Want to explore more?** Visit the [Node.js GitHub repository](https://github.com/nodejs/node).

🚀 Happy Coding!
