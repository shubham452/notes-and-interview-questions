**1. Event Loop**

- The event loop is responsible for managing asynchronous operations in
  JavaScript.

- It continuously checks the **Call Stack** and the **Task Queue** to
  determine what to execute next.

- If the call stack is empty, it takes the first task from the queue and
  pushes it to the call stack.

**2. Call Stack**

- A data structure that records the function calls in the order they
  need to be executed.

- Functions are pushed to the stack when called and popped off when
  completed.

**Example:**

function foo() {

console.log(\"foo\");

}

function bar() {

foo();

console.log(\"bar\");

}

bar();

// Call Stack:

// bar() -\> foo() -\> console.log(\"foo\") -\> console.log(\"bar\")

**3. Web APIs**

- Provided by the browser (or environment), allowing asynchronous
  operations like setTimeout, DOM events, fetch, etc.

- These do not run in the call stack directly but are handled outside by
  the environment.

**Example:**

console.log(\"Start\");

setTimeout(() =\> console.log(\"Timer\"), 0);

console.log(\"End\");

// Output:

// Start

// End

// Timer

**4. Task Queue / Job Queue**

- **Task Queue:** Holds callback functions from asynchronous operations
  (like setTimeout, setInterval).

- **Job Queue (Microtask Queue):** Holds promises and asynchronous tasks
  that are prioritized over the task queue.

- The **Event Loop** gives preference to the **Job Queue**.

**5. Microtasks vs. Macrotasks**

| **Microtasks**                                       | **Macrotasks**                                 |
|------------------------------------------------------|------------------------------------------------|
| Processed immediately after the call stack is empty. | Processed after microtasks.                    |
| Includes: Promises, process.nextTick.                | Includes: setTimeout, setInterval, DOM events. |
| Higher priority.                                     | Lower priority.                                |

**Example:**

console.log(\"Start\");

setTimeout(() =\> console.log(\"Macrotask\"), 0);

Promise.resolve().then(() =\> console.log(\"Microtask\"));

console.log(\"End\");

// Output:

// Start

// End

// Microtask

// Macrotask

**6. Timers and Intervals**

- **setTimeout():** Executes a function after a specified delay.

- **setInterval():** Repeats execution at specified intervals.

- **clearTimeout():** Cancels a timeout.

- **clearInterval():** Cancels an interval.

**Example:**

const timeoutId = setTimeout(() =\> console.log(\"Timeout!\"), 1000);

clearTimeout(timeoutId); // Cancels the timeout

const intervalId = setInterval(() =\> console.log(\"Interval!\"), 1000);

clearInterval(intervalId); // Cancels the interval

**7. requestAnimationFrame()**

- Optimizes animations by calling a callback just before the next
  repaint.

- More efficient than setTimeout for animations.

- Automatically pauses when the tab is not active.

**Example:**

let pos = 0;

function animate() {

pos += 1;

console.log(\"Moving to:\", pos);

if (pos \< 10) {

requestAnimationFrame(animate);

}

}

requestAnimationFrame(animate);

**Example of Event Loop Handling:**

console.log(\"Start\");

setTimeout(() =\> console.log(\"setTimeout\"), 0);

Promise.resolve().then(() =\> console.log(\"Promise\"));

console.log(\"End\");

// Output:

// Start

// End

// Promise

// setTimeout

**Explanation:**

1.  **Synchronous tasks** (like console.log) go to the **Call Stack**.

2.  **Microtasks** (like the resolved promise) go to the **Job Queue**.

3.  **Macrotasks** (like setTimeout) go to the **Task Queue**.

4.  The **Event Loop** processes the **Call Stack** first, then **Job
    Queue** (Microtasks), and finally **Task Queue** (Macrotasks).
