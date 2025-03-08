**🚀 Hoisting in JavaScript**

Hoisting is a **JavaScript mechanism** where **variables and function
declarations are moved to the top** of their containing scope **during
compilation**. This means you can use functions and variables **before**
they are declared in the code.

**1️⃣ What Gets Hoisted?**

✅ **Hoisted:**

- **Function Declarations** (function myFunc() {})

- **Variable Declarations** (var x;) but **not the assignment!**

❌ **Not Hoisted:**

- **Function Expressions** (const myFunc = function() {};)

- **Arrow Functions** (const myFunc = () =\> {};)

- **let and const variables** (they exist in the **Temporal Dead Zone**
  until initialized)

**2️⃣ Hoisting with var**

Variables declared with var are hoisted, but **only the declaration**,
not the value.

**🔹 Example**

console.log(name); // undefined (NOT an error)

var name = \"Alice\";

console.log(name); // \"Alice\"

**🔹 How JavaScript Sees It (Behind the Scenes)**

var name; // Hoisted to the top with \"undefined\"

console.log(name); // undefined

name = \"Alice\"; // Assignment happens later

console.log(name); // \"Alice\"

⚠️ **Only declarations are hoisted, NOT initializations!**

**3️⃣ Hoisting with let and const**

Variables declared with let and const are **hoisted**, but they are in
the **Temporal Dead Zone (TDZ)** until assigned a value.

**🔹 Example**

console.log(age); // ❌ ReferenceError: Cannot access \'age\' before
initialization

let age = 25;

**🔹 How JavaScript Sees It**

// Hoisted but in Temporal Dead Zone

let age; // Hoisted, but in TDZ

console.log(age); // ❌ ReferenceError

age = 25; // Initialization happens here

⛔ **Using let and const before their declaration causes a
ReferenceError.**

**4️⃣ Hoisting with Functions**

**✅ Function Declarations are Hoisted**

console.log(greet()); // ✅ \"Hello!\"

function greet() { // Function is fully hoisted

return \"Hello!\";

}

console.log(greet()); // ✅ \"Hello!\"

**5️⃣ Function Expressions & Arrow Functions Are NOT Hoisted**

Functions assigned to variables (function expressions and arrow
functions) **are NOT hoisted**.

**🔹 Function Expression Example**

console.log(sum(2, 3)); // ❌ TypeError: sum is not a function

var sum = function(a, b) {

return a + b;

};

🔹 **How JavaScript Sees It**

var sum; // Hoisted but undefined

console.log(sum(2, 3)); // ❌ TypeError

sum = function(a, b) { return a + b; }; // Assignment happens here

Since sum is hoisted as undefined, calling it before assignment results
in an error.

**🔹 Arrow Function Example**

console.log(multiply(3, 4)); // ❌ TypeError: multiply is not a function

const multiply = (a, b) =\> a \* b;

✅ **Solution:** Declare **function expressions** and **arrow
functions** **before** using them.

**6️⃣ Hoisting in Different Scopes**

Hoisting works **inside functions and blocks** too.

**🔹 Example in Function Scope**

function test() {

console.log(x); // undefined (hoisted)

var x = 10;

console.log(x); // 10

}

test();

🛑 **Variables declared with var inside functions are hoisted within
that function.**

**🔹 Example in Block Scope**

if (true) {

console.log(y); // ❌ ReferenceError

let y = 5;

}

Variables declared with let and const are **block-scoped** and not
accessible before declaration.

**7️⃣ Best Practices to Avoid Hoisting Issues**

✅ **Use let and const instead of var**

// Bad

var count = 10;

// Good

let count = 10;

const max = 100;

✅ **Declare functions before using them**

// ❌ Avoid

console.log(add(3, 4));

const add = (a, b) =\> a + b;

// ✅ Do this

const add = (a, b) =\> a + b;

console.log(add(3, 4));

✅ **Write functions at the top of their scope**

function calculateTotal(price) {

return price \* 1.1;

}

console.log(calculateTotal(100)); // ✅ Works fine

**🚀 Summary Table**

| **Concept**          | **Hoisted?** | **Usable Before Declaration?** |
|----------------------|--------------|--------------------------------|
| var                  | ✅ Yes       | ❌ Only as undefined           |
| let                  | ✅ Yes       | ❌ Temporal Dead Zone (TDZ)    |
| const                | ✅ Yes       | ❌ Temporal Dead Zone (TDZ)    |
| Function Declaration | ✅ Yes       | ✅ Yes                         |
| Function Expression  | ❌ No        | ❌ No                          |
| Arrow Function       | ❌ No        | ❌ No                          |

**🔹 Final Thoughts**

- var gets hoisted **but as undefined**, leading to **unexpected
  behavior**.

- let and const are **hoisted but remain in the Temporal Dead Zone**, so
  accessing them before declaration causes an error.

- **Function declarations are fully hoisted**, so they can be called
  before declaration.

- **Function expressions and arrow functions are NOT hoisted**, so they
  must be declared before use.
