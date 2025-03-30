**🔥 Currying in JavaScript**

**🚀 What is Currying?**

Currying is a technique in functional programming where a function
**takes multiple arguments one at a time instead of all at once**.
Instead of taking all arguments in a single call, a curried function
returns a **new function** that takes the next argument, and so on.

**1️⃣ Basic Example of Currying**

Let\'s transform a normal function into a **curried** function.

**🔹 Normal Function (Non-Curried)**

function add(a, b, c) {

return a + b + c;

}

console.log(add(2, 3, 5)); // 10

**🔹 Curried Version**

function add(a) {

return function (b) {

return function (c) {

return a + b + c;

};

};

}

console.log(add(2)(3)(5)); // 10

💡 **What Happened?**

1.  add(2) returns a function waiting for b.

2.  add(2)(3) returns another function waiting for c.

3.  add(2)(3)(5) returns the final result.

**2️⃣ Why Use Currying?**

**✅ Code Reusability**

Currying allows partial application, meaning we can **reuse** functions
with preset arguments.

const addFive = add(5); // Fixes \`a = 5\`

console.log(addFive(2)(3)); // 10

console.log(addFive(10)(5)); // 20

🔹 **Why?**

- We create a specialized version of add where a = 5, making it
  reusable.

**3️⃣ Real-World Examples**

**🔹 Example 1: Logger Function**

A **custom logger** with different log levels.

function logger(level) {

return function (message) {

console.log(\`\[\${level}\] \${message}\`);

};

}

const errorLog = logger(\"ERROR\");

const infoLog = logger(\"INFO\");

errorLog(\"Something went wrong!\"); // \[ERROR\] Something went wrong!

infoLog(\"Application started.\"); // \[INFO\] Application started.

**🔹 Example 2: Filtering Data**

A curried function to filter an array based on a condition.

const filterBy = (property) =\> (value) =\> (arr) =\> {

return arr.filter(item =\> item\[property\] === value);

};

const users = \[

{ name: \"Alice\", role: \"admin\" },

{ name: \"Bob\", role: \"user\" },

{ name: \"Charlie\", role: \"admin\" }

\];

const filterByRole = filterBy(\"role\"); // Pre-set property

const getAdmins = filterByRole(\"admin\"); // Pre-set value

console.log(getAdmins(users));

// \[{ name: \"Alice\", role: \"admin\" }, { name: \"Charlie\", role:
\"admin\" }\]

**4️⃣ Converting a Normal Function to Curried Function**

We can convert a function to a curried version using a **higher-order
function**.

function curry(func) {

return function curried(\...args) {

if (args.length \>= func.length) {

return func.apply(this, args); // If all arguments are provided, execute
function

} else {

return (\...nextArgs) =\> curried(\...args, \...nextArgs); // Else
return a function

}

};

}

function multiply(a, b, c) {

return a \* b \* c;

}

const curriedMultiply = curry(multiply);

console.log(curriedMultiply(2)(3)(4)); // 24

console.log(curriedMultiply(2, 3)(4)); // 24

console.log(curriedMultiply(2, 3, 4)); // 24

✅ **This works with both partial and full argument calls!**

**5️⃣ Currying vs Partial Application**

- **Currying**: Transforms a function into a series of functions that
  take one argument at a time.

- **Partial Application**: Pre-fills some arguments but still allows
  multiple arguments in later calls.

**🔹 Example of Partial Application**

function partialMultiply(a, b, c) {

return a \* b \* c;

}

const multiplyByTwo = partialMultiply.bind(null, 2); // Fix \`a = 2\`

console.log(multiplyByTwo(3, 4)); // 24

💡 **Difference**: Currying always **returns functions until all
arguments are provided**, while partial application **fills some
arguments and keeps the function callable normally**.

**6️⃣ Key Takeaways**

✅ **Currying helps create reusable, modular, and composable
functions.**  
✅ **It transforms a function into multiple smaller functions that take
one argument at a time.**  
✅ **It enables functional programming techniques like function
composition and partial application.**
