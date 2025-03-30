**🚀 JavaScript Functions Deep Dive**

JavaScript functions can be **named**, **anonymous**, **arrow
functions**, **function expressions**, **IIFEs**, or **function
constructors**. Let\'s break them down one by one.

**1️⃣ Named Functions**

A **named function** is a function that has a **name** and can be
**called by that name**.

✅ **Key Features:**

- Can be reused multiple times.

- Can be called **before** its declaration due to **hoisting**.

- Useful for **debugging** as the function name appears in error
  messages.

**🔹 Example**

function greet(name) {

return \`Hello, \${name}!\`;

}

console.log(greet(\"Alice\")); // \"Hello, Alice!\"

✅ **Hoisting Example** (Named functions are hoisted)

console.log(square(4)); // ✅ Works due to hoisting

function square(num) {

return num \* num;

}

**2️⃣ Anonymous Functions**

An **anonymous function** is a function **without a name**.

✅ **Key Features:**

- Often assigned to a variable or used as a callback.

- Cannot be called before declaration (not hoisted like named
  functions).

**🔹 Example**

const greet = function(name) {

return \`Hello, \${name}!\`;

};

console.log(greet(\"Bob\")); // \"Hello, Bob!\"

🔹 **Common Usage**: Used as **callback functions**

setTimeout(function() {

console.log(\"This runs after 2 seconds\");

}, 2000);

**3️⃣ Arrow Functions (() =\> {})**

An **arrow function** is a shorter way to write functions.

✅ **Key Features:**

- **No this binding** (inherits this from the surrounding scope).

- **Implicit return** (if there's only one statement).

- **Cannot be used as constructors** (new doesn't work).

- **Cannot use arguments object** (use rest parameters instead).

**🔹 Example**

const greet = (name) =\> \`Hello, \${name}!\`;

console.log(greet(\"Charlie\")); // \"Hello, Charlie!\"

🔹 **With multiple parameters & statements**

const add = (a, b) =\> {

let sum = a + b;

return sum;

};

console.log(add(5, 3)); // 8

🔹 **Implicit Return (No {})**

const square = x =\> x \* x;

console.log(square(4)); // 16

🔹 **this Behavior in Arrow Functions**

const obj = {

name: \"Alice\",

regularFunc: function() {

console.log(this.name); // ✅ \"Alice\"

},

arrowFunc: () =\> {

console.log(this.name); // ❌ \`undefined\` (no \`this\` binding)

}

};

obj.regularFunc();

obj.arrowFunc();

**4️⃣ Function Expressions**

A **function expression** is when a function is assigned to a variable.

✅ **Key Features:**

- Can be **named** or **anonymous**.

- Not hoisted like function declarations.

**🔹 Example**

const multiply = function(x, y) {

return x \* y;

};

console.log(multiply(3, 4)); // 12

🔹 **Named Function Expression**

const factorial = function fact(n) {

return n === 0 ? 1 : n \* fact(n - 1);

};

console.log(factorial(5)); // 120

⚠️ **Cannot call fact() outside the function scope.**

**5️⃣ Immediately Invoked Function Expressions (IIFE)**

An **IIFE** is a function that is **executed immediately** after it is
defined.

✅ **Key Features:**

- Prevents polluting the **global scope**.

- Executes **only once**.

**🔹 Example**

(function() {

console.log(\"This runs immediately!\");

})(); // \"This runs immediately!\"

🔹 **Arrow Function IIFE**

(() =\> {

console.log(\"Arrow function IIFE!\");

})();

🔹 **IIFE with Parameters**

(function(name) {

console.log(\`Hello, \${name}!\`);

})(\"David\");

**6️⃣ Function Constructors (new Function())**

A **function constructor** dynamically creates a new function.

✅ **Key Features:**

- Created using new Function(arg1, arg2, \..., functionBody).

- Function body is defined as a string.

- **Not recommended** (slower, no lexical scope).

**🔹 Example**

const add = new Function(\"a\", \"b\", \"return a + b\");

console.log(add(2, 3)); // 5

🔹 **Major Downsides:**

- Functions created this way **don\'t have access to local variables**.

- Always runs in the **global scope**.

**🚀 Summary**

| **Type**                 | **Hoisted?** | **this Binding** | **Use Case**                                |
|--------------------------|--------------|------------------|---------------------------------------------|
| **Named Function**       | ✅ Yes       | Dynamic          | Reusable functions                          |
| **Anonymous Function**   | ❌ No        | Dynamic          | One-time use, callbacks                     |
| **Arrow Function**       | ❌ No        | Inherits         | Short syntax, this in callbacks             |
| **Function Expression**  | ❌ No        | Dynamic          | Assigning functions to variables            |
| **IIFE**                 | ❌ No        | Dynamic          | Avoid polluting global scope                |
| **Function Constructor** | ❌ No        | Global Scope     | Dynamic function creation (not recommended) |

**🚀 When to Use What?**

- **Named functions** → When defining reusable functions.

- **Anonymous functions** → For **callbacks**, event handlers, and
  one-time-use cases.

- **Arrow functions** → When using this **inside objects** and for
  **concise syntax**.

- **Function expressions** → When you need **functions as values**
  (e.g., storing in variables).

- **IIFE** → When you **need to execute code immediately** without
  polluting the global scope.

- **Function constructors** → **Avoid using them** unless dynamically
  creating functions from strings.
