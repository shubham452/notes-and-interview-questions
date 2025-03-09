**🚀 JavaScript Execution Context Explained**

When JavaScript runs code, it does so within an **Execution Context**. Understanding execution contexts is crucial for knowing **how JavaScript handles variables, functions, and scopes**.

-----
**📌 What is Execution Context?**

An **Execution Context (EC)** is an environment in which JavaScript code is executed. It determines how **variables and functions** are stored and accessed during execution.

**Types of Execution Contexts:**

1. **Global Execution Context (GEC)**
   1. Created when JavaScript starts execution (default context).
   1. Represents the global scope (window in browsers, global in Node.js).
   1. Variables and functions declared outside any function belong here.
1. **Function Execution Context (FEC)**
   1. Created whenever a function is called.
   1. Each function has its **own execution context**.
1. **Eval Execution Context**
   1. Created when using eval() (not recommended due to security risks).
-----
**📌 Execution Context Lifecycle**

Each execution context goes through **three phases**:

**1️⃣ Creation Phase (Memory Allocation)**

- JavaScript **allocates memory** for variables and functions.
- var variables are initialized with undefined (hoisting).
- Function declarations are **fully hoisted**.
- let and const variables are in the **Temporal Dead Zone (TDZ)**.

**2️⃣ Execution Phase (Code Execution)**

- JavaScript assigns values to variables and executes function calls.

**3️⃣ Destruction Phase (Context Removal)**

- Once execution is complete, the context is **popped off the Call Stack**.
-----
**📌 Execution Context in Action**

Let's break it down with an example:

var x = 10;

function foo() {

`    `var y = 20;

`    `console.log(x + y);

}

foo();

console.log("Done");

**Execution Steps**

1️⃣ **Global Execution Context (GEC) is created**

- var x = 10; (Memory allocated, initially undefined, then set to 10).
- foo() function is stored in memory.

2️⃣ **Function Execution Context (FEC) is created when foo() is called**

- var y = 20; is stored in the local function scope.
- console.log(x + y); runs and outputs 30.

3️⃣ **FEC is destroyed** after execution.
4️⃣ console.log("Done"); executes.

✅ **Final Output:**

30

Done

-----
**📌 Call Stack & Execution Context**

JavaScript uses the **Call Stack** to manage execution contexts.

function first() {

`    `console.log("First");

`    `second();

}

function second() {

`    `console.log("Second");

}

first();

console.log("Done");

🔹 **Execution Order (Call Stack Operations)**:

1. first() is called → **Pushed to Call Stack**.
1. console.log("First") → Runs & Pops.
1. second() is called → **Pushed to Call Stack**.
1. console.log("Second") → Runs & Pops.
1. first() completes → **Popped from Call Stack**.
1. console.log("Done") executes.

✅ **Final Output:**

First

Second

Done

-----
**📌 Key Takeaways**

✅ **Every JavaScript execution happens inside an execution context.**
✅ **The Global Execution Context (GEC) is created first.**
✅ **Each function call creates a new Function Execution Context (FEC).**
✅ **Execution contexts follow a "Creation → Execution → Destruction" cycle.**
✅ **The Call Stack keeps track of all execution contexts.**

