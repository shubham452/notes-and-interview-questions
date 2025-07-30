**🚀 Closures in JavaScript**

A **closure** is a function that **remembers the variables from its
outer scope** even after the outer function has finished executing.

Closures are powerful because they **allow functions to retain access to
variables from their lexical scope**, even when executed outside that
scope.

**1️⃣ Basic Example of Closures**

function outerFunction() {

let outerVariable = \"I am from outer scope\";

function innerFunction() {

console.log(outerVariable); // ✅ Accesses outerVariable even after
outerFunction is done

}

return innerFunction;

}

const closureFunction = outerFunction(); // outerFunction executes and
returns innerFunction

closureFunction(); // ✅ \"I am from outer scope\"

**🔹 How It Works**

1.  outerFunction is executed, creating a new scope.

2.  Inside outerFunction, outerVariable is defined.

3.  innerFunction is defined inside outerFunction and **has access to
    outerVariable**.

4.  outerFunction **returns** innerFunction, which is stored in
    closureFunction.

5.  When we call closureFunction(), it **remembers the scope** in which
    it was created and logs \"I am from outer scope\".

**2️⃣ Closures Maintain State**

Closures **can store state** across function calls.

**🔹 Example: Counter Using Closures**

function createCounter() {

let count = 0; // Private variable

return function () {

count++;

console.log(\`Count: \${count}\`);

};

}

const counter1 = createCounter();

counter1(); // Count: 1

counter1(); // Count: 2

const counter2 = createCounter();

counter2(); // Count: 1 (separate instance)

counter2(); // Count: 2

🔹 **Why?**

- Each call to createCounter() creates a **new instance** of count, so
  counter1 and counter2 have separate counters.

**3️⃣ Practical Uses of Closures**

**✅ Data Hiding & Encapsulation**

Closures allow you to **hide data** and prevent it from being modified
directly.

function secretHolder(secret) {

return {

getSecret: function () {

return secret;

}

};

}

const mySecret = secretHolder(\"I love JavaScript\");

console.log(mySecret.getSecret()); // \"I love JavaScript\"

console.log(mySecret.secret); // ❌ undefined (cannot access directly)

💡 **Why?**

- secret is not accessible directly but is **remembered** by the
  returned function.

**✅ Function Factories**

Closures can be used to **create multiple functions with preset
behavior**.

function multiplyBy(factor) {

return function (number) {

return number \* factor;

};

}

const double = multiplyBy(2);

console.log(double(5)); // 10

const triple = multiplyBy(3);

console.log(triple(5)); // 15

💡 **Why?**

- double and triple each **remember** their own factor.

**✅ Event Listeners Using Closures**

Closures can help maintain **state in event handlers**.

function attachEventListener() {

let count = 0;

document.getElementById(\"myButton\").addEventListener(\"click\",
function () {

count++;

console.log(\`Button clicked \${count} times\`);

});

}

attachEventListener();

💡 **Why?**

- The event listener **remembers count** even after
  attachEventListener() has finished execution.

**4️⃣ Closures and Loops**

Closures can sometimes cause **unexpected behavior in loops**.

**🔹 Example: Using var (Unexpected Output)**

for (var i = 1; i \<= 3; i++) {

setTimeout(function () {

console.log(i);

}, 1000);

}

⛔ **Output (after 1 second)**:

CopyEdit

4

4

4

🔹 **Why?**

- var is function-scoped, so **all closures share the same i (which is 4
  when setTimeout runs).**

**🔹 Fix Using let**

for (let i = 1; i \<= 3; i++) {

setTimeout(function () {

console.log(i);

}, 1000);

}

✅ **Output**:

1

2

3

💡 **Why?**

- let creates a new **block-scoped** variable for each iteration.

**5️⃣ Closures in setTimeout**

Closures are often used in setTimeout() functions.

**✅ Delayed Execution**

function delayedMessage(message, delay) {

setTimeout(function () {

console.log(message);

}, delay);

}

delayedMessage(\"Hello after 2 seconds\", 2000);

💡 **Why?**

- The callback inside setTimeout **remembers** message even after
  delayedMessage() has executed.

**🚀 Summary**

✅ **Closures allow functions to \"remember\" variables from their outer
scope even after execution.**  
✅ **They are used for:**

- Data hiding (private variables)

- Function factories (creating pre-configured functions)

- Maintaining state in event handlers & loops

- Delayed execution with setTimeout

**🔹 Key Takeaways**

| **Concept**                   | **Explanation**                                                    |
|-------------------------------|--------------------------------------------------------------------|
| **Closure**                   | A function that remembers variables from its outer scope.          |
| **Lexical Scope**             | Functions can access variables from their parent function.         |
| **State Persistence**         | Variables inside a closure remain even after the function returns. |
| **Avoiding Global Variables** | Helps keep variables encapsulated.                                 |


Here are notes on **Closures in JavaScript** along with a coding example, drawing from the provided sources:

---

### **Notes on Closures in JavaScript**

1.  **Definition of a Closure**
    *   In simple terms, a **closure** means that a **function along with its lexical environment forms a closure**.
    *   It is described as a **function bundled together with its surrounding state or lexical environment**.
    *   This implies that a function remembers its lexical scope even when it is executed outside that scope.

2.  **Lexical Environment / Lexical Scope**
    *   **Lexical scope** refers to **where a function or variable is physically present in the code**. It's the environment in which the code is written or defined.
    *   Every function and block has its own lexical scope, and these scopes can be nested.
    *   When a function is defined, it "remembers" its lexical environment (i.e., the variables and functions that were available in its scope at the time of its creation).

3.  **Core Concept: Remembering the Lexical Environment**
    *   The most significant aspect of closures is that **even after an outer function's execution context has finished and conceptually "disappeared," the inner function (the closure) still retains a reference to the variables in its parent's lexical scope**.
    *   This means that the inner function can **access and manipulate** these outer variables even when it's invoked much later and from a different part of the code.

4.  **How Closures Form and Behave**
    *   When an inner function is returned from an outer function, it doesn't just return the function's code; it returns the function **along with its entire lexical environment**.
    *   This "bundle" of function code and its preserved lexical scope is what constitutes the closure.
    *   The variables from the outer scope are not just passed by value; the closure holds a **reference** to these variables, meaning if their value changes, the closure will see the updated value.

5.  **Importance and Use Cases of Closures**
    *   Closures are a **fundamental concept in JavaScript** and are the basis for many powerful patterns.
    *   They enable functionalities like **currying** (transforming a function that takes multiple arguments into a sequence of functions that each take a single argument) and **higher-order functions**.
    *   They are crucial for **module design patterns** and for achieving **data privacy or encapsulation** (hiding private variables and functions from the global scope).
    *   Other applications include **debouncing** and **memoization**.
    *   Understanding closures is considered a **very common and important interview question**.

---

### **Coding Example: Basic Closure**

This example demonstrates how an inner function, even after being returned from its parent, maintains access to variables from its parent's lexical scope.

```javascript
// 1. Define an outer function 'x'
function x() {
  var a = 7; // 'a' is a variable in the lexical scope of function 'x'

  // 2. Define an inner function 'y'
  //    'y' is lexically inside 'x', so it has access to 'a'.
  function y() {
    console.log(a); // 'y' refers to 'a' from its lexical parent 'x'
  }

  // 3. Instead of calling 'y' immediately, 'x' returns 'y'.
  //    This is where the magic of closure happens.
  return y;
}

// 4. Call function 'x' and store its return value (which is function 'y')
//    into a variable named 'z'.
//    At this point, the execution context of 'x' is conceptually "long gone".
var z = x();

// 5. Now, call 'z'. Since 'z' holds function 'y', we are essentially calling 'y'.
//    Despite 'x' having finished execution, 'y' (via 'z') still remembers 'a'.
console.log("Calling the function 'z' (which is 'y') after 'x' has finished:");
z(); // Expected Output: 7
```

**Explanation of the Example:**

1.  **`function x()` is defined**: Inside `x`, a `var` variable `a` is declared with a value of `7`.
2.  **`function y()` is defined INSIDE `x()`**: Because `y` is defined inside `x`, its lexical environment includes `a`.
3.  **`x()` returns `y`**: Instead of executing `y` immediately, `x` returns the function `y` itself.
4.  **`var z = x()`**: When `x()` is called, it executes, `a` is initialized, and then `y` is returned. The returned `y` function is assigned to `z`. Crucially, at this point, the execution context of `x` is popped off the call stack and considered "gone". You might expect `a` to be garbage collected since `x` is done.
5.  **`z()` is called**: When `z()` is called (which is actually `y()`), it still needs to find the value of `a`. This is where the **closure** comes into play:
    *   The `y` function, when it was returned from `x`, **bundled itself together with its lexical environment**.
    *   This bundle (the closure) means that `y` still holds a **reference** to the variable `a` from `x`'s scope, even though `x` has completed its execution.
    *   Therefore, `y` successfully accesses `a` and prints `7` to the console.

This mechanism is why closures are so powerful, allowing functions to "remember" data from their creation environment, even when that environment no longer exists in the call stack.
