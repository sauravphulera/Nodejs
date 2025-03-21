# Episode-06 | libuv & Async IO

## Introduction
One of the key points we came across in the first episode was the statement that:
> "Node.js has an event-driven architecture capable of asynchronous I/O."

This episode focuses on explaining that concept.

---
## Understanding JavaScript Fundamentals

### What is a Thread?
A thread is the smallest unit of execution within a process in an operating system. It represents a sequence of instructions that can run independently. Multiple threads can exist within a single process, sharing the same memory space while executing separately, improving efficiency and responsiveness.

Threads can be categorized as:
1. **Single-threaded**
2. **Multi-threaded**

### What Type of Threading Does JavaScript Use?
JavaScript is a **synchronous, single-threaded** language. This means that code is executed **line by line** in a single thread.

- In languages like **C++ or Java**, multiple threads can run simultaneously.
- JavaScript executes code in sequence, meaning **line 2 executes only after line 1 has finished.**

---
## Synchronous vs Asynchronous JavaScript

### What is a Synchronous System?
- Tasks are completed **one after another**.
- Think of it as using **one hand** to complete **10 tasks**—each task must be finished before moving to the next.
- An order can only be fulfilled **after the previous one is completed**.

### What is an Asynchronous System?
- Tasks run **independently**.
- Imagine having **10 hands** for **10 tasks**—each can be completed separately.
- Orders do not have to wait for each other; they are completed as soon as resources are available.

JavaScript itself is **synchronous**, but Node.js enables it to handle **asynchronous operations**.

---
## JavaScript Engine and Execution

### Components Inside the JS Engine
1. **Call Stack** - Executes synchronous code.
2. **Memory Heap** - Stores variables, numbers, and functions.
3. **Garbage Collector** - Automatically removes unused variables.

### How Synchronous Code Executes
1. **Step 1:** Global Execution Context (GEC) is created.
2. **Step 2:** Memory Creation Phase:
   - Variables and functions are stored in memory with `undefined` values initially.
3. **Step 3:** Code Execution Phase:
   - Variables get assigned values.
   - Functions execute and return values.
4. **Step 4:** Function Execution Context Creation:
   - Functions create a new execution context on top of the call stack.
5. **Step 5:** Memory and Execution Inside Functions:
   - Variables inside functions get stored and used.
   - The function completes execution and is removed from the call stack.
6. **Step 6:** Resuming Global Execution Context.
7. **Step 7:** Once all code is executed, the call stack becomes empty.

---
## How Asynchronous Code is Executed
The JavaScript engine **alone** cannot handle asynchronous tasks—it needs **Node.js and libuv**.

### What is libuv?
- **libuv** is a library that provides **event-driven asynchronous I/O** capabilities to Node.js.
- It enables Node.js to **offload operations** such as:
  - API calls
  - File operations
  - Timers

### How libuv Works:
1. The JS engine **encounters an API call**.
2. It delegates the task to **libuv**.
3. **libuv registers the API call** and its callback function.
4. JavaScript continues executing the rest of the code **without waiting**.
5. Once the API response is ready, **libuv notifies JavaScript** to execute the callback.

### Handling Asynchronous Operations
- `setTimeout`: libuv registers the timer and notifies JS when it expires.
- File System Operations: libuv performs I/O operations in the background and sends results to JS.
- Function Execution: JavaScript continues synchronous execution while libuv manages asynchronous tasks.

### Important Concept: Garbage Collection
- When a function execution context is removed from the call stack, its **memory may be cleared** by the garbage collector.
- The **call stack becomes empty** once all execution is complete.

---
## Summary
- **JavaScript is single-threaded** but uses **libuv in Node.js** to handle **asynchronous operations**.
- **libuv enables non-blocking I/O**.
- The **event loop** ensures JavaScript continues executing while asynchronous tasks are handled in the background.

By leveraging libuv, **Node.js efficiently manages asynchronous I/O operations**, making it powerful and scalable for real-world applications.
