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
