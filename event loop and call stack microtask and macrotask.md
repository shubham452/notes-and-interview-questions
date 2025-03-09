**🚀 JavaScript Event Loop, Call Stack, Microtasks & Macrotasks Explained**

JavaScript is **single-threaded**, meaning it can execute **one task at a time**. But thanks to **asynchronous execution**, it can handle non-blocking tasks using the **Event Loop**.

-----
**🌀 Event Loop Overview**

The **Event Loop** is the mechanism that allows JavaScript to:

1. Execute **synchronous** code first.
1. Handle **asynchronous** operations (like setTimeout, Promises, and event listeners).
1. Manage tasks via **Call Stack**, **Microtasks Queue**, and **Macrotasks Queue**.
-----
**📌 Call Stack**

The **Call Stack** is a **LIFO (Last In, First Out)** structure where JavaScript keeps track of function execution.
✅ When a function is called, it is **pushed** onto the stack.
✅ When it finishes execution, it is **popped** off the stack.

**Example:**

function first() {

`    `console.log("First");

}

function second() {

`    `console.log("Second");

}

first();

second();

console.log("Done");

**Execution order (Call Stack operations):**

1\. first() → Pushed to Call Stack

2\. console.log("First") → Executed & popped

3\. first() → Popped

4\. second() → Pushed to Call Stack

5\. console.log("Second") → Executed & popped

6\. second() → Popped

7\. console.log("Done") → Executed

✅ Output:

First

Second

Done

🛑 **JavaScript is synchronous by default** → One task at a time.

-----
**📌 Macrotasks vs Microtasks**

JavaScript handles **asynchronous tasks** via two queues:

1. **Macrotasks Queue** (also called Task Queue):
   1. Includes: setTimeout, setInterval, setImmediate, I/O operations, MessageChannel
   1. Executed **AFTER** all synchronous code and Microtasks.
1. **Microtasks Queue** (higher priority than Macrotasks):
   1. Includes: Promises (then/catch/finally), MutationObserver, queueMicrotask
   1. Executed **immediately after the Call Stack is empty**, before Macrotasks.
-----
**📌 Event Loop Execution Order**

1️⃣ Execute **all synchronous** code.
2️⃣ **Empty the Call Stack**.
3️⃣ Process **all Microtasks (Promises, queueMicrotask)**.
4️⃣ Process **one Macrotask (setTimeout, setInterval, etc.)**.
5️⃣ Repeat steps **3 & 4** until all tasks are done.

-----
**📌 Example: Microtasks vs. Macrotasks**

console.log("1️⃣ Start");

setTimeout(() => console.log("5️⃣ setTimeout"), 0);

Promise.resolve().then(() => console.log("3️⃣ Promise"));

console.log("2️⃣ End");

🔹 **Execution breakdown:**

1. console.log("1️⃣ Start") → Sync (Call Stack) ✅
1. setTimeout(..., 0) → Goes to **Macrotask Queue** ⏳
1. Promise.resolve().then(...) → Goes to **Microtask Queue** ⏳
1. console.log("2️⃣ End") → Sync (Call Stack) ✅
1. Microtask queue runs: console.log("3️⃣ Promise") ✅
1. Macrotask queue runs: console.log("5️⃣ setTimeout") ✅

✅ **Output:**

1️⃣ Start

2️⃣ End

3️⃣ Promise

5️⃣ setTimeout

🛑 **Microtasks run before Macrotasks!**

-----
**📌 Real-World Example**

console.log("Start");

setTimeout(() => console.log("Timeout"), 0);

Promise.resolve().then(() => console.log("Promise 1"));

Promise.resolve().then(() => {

`    `console.log("Promise 2");

`    `setTimeout(() => console.log("Inner Timeout"), 0);

});

console.log("End");

✅ **Execution order:** 1️⃣ console.log("Start") ✅
2️⃣ setTimeout(..., 0) → **Macrotask Queue** ⏳
3️⃣ Promise.resolve().then(...) → **Microtask Queue** ⏳
4️⃣ Promise.resolve().then(...) → **Microtask Queue** ⏳
5️⃣ console.log("End") ✅
6️⃣ **Microtasks run** → Promise 1 ✅
7️⃣ **Microtasks continue** → Promise 2 ✅
8️⃣ setTimeout(..., 0) (Inner) → **Macrotask Queue** ⏳
9️⃣ **Macrotasks run** → Timeout ✅
🔟 **Macrotasks continue** → Inner Timeout ✅

✅ **Final Output:**

Start

End

Promise 1

Promise 2

Timeout

Inner Timeout

-----
**🎯 Summary**

|**Concept**|**Description**|
| :-: | :-: |
|**Call Stack**|Handles synchronous code execution (LIFO).|
|**Microtasks Queue**|Includes Promises & runs **before** Macrotasks.|
|**Macrotasks Queue**|Includes setTimeout, runs **after** Microtasks.|
|**Event Loop**|Executes tasks in order: Call Stack → Microtasks → Macrotasks.|

-----
**🚀 Key Takeaways**

✅ **JavaScript is single-threaded** but uses an **Event Loop** for async tasks.
✅ **Microtasks (Promises) run before Macrotasks (setTimeout).**
✅ **Call Stack** executes sync code first, then defers async tasks.
✅ **Understanding the Event Loop helps avoid race conditions & optimize performance.**

