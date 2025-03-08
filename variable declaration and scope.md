1️⃣ var (Function Scoped)

Can be re-declared and updated.

Has function scope (accessible throughout the function where it's declared).

Hoisted to the top of the function with a default value of undefined.

Not block-scoped, meaning it ignores {} blocks.

📌 Example:

function testVar() {

&nbsp;   if (true) {

&nbsp;       var x = 10;

&nbsp;   }

&nbsp;   console.log(x); // ✅ 10 (Still accessible outside the block)

}

testVar();

🔴 Problem with var: Can cause unexpected behavior due to lack of block scope.

2️⃣ let (Block Scoped)

Can be updated but not re-declared in the same scope.

Has block scope (only accessible inside {} where declared).

Hoisted but not initialized (can't access before declaration).

📌 Example:

function testLet() {

&nbsp;   if (true) {

&nbsp;       let y = 20;

&nbsp;   }

&nbsp;   console.log(y); // ❌ ReferenceError: y is not defined

}

testLet();

✅ Safer than var because it's limited to the block.

3️⃣ const (Block Scoped, Immutable)

Cannot be updated or re-declared.

Must be initialized when declared.

Stores references (for objects/arrays, properties can change, but the reference cannot).

📌 Example:

const z = 30;

z = 40; // ❌ TypeError: Assignment to constant variable.

const obj = { name: "John" };

obj.name = "Doe"; // ✅ Allowed (modifying object property)

console.log(obj); // { name: "Doe" }

🟠 Scope in JavaScript

Scope determines where variables can be accessed.

1️⃣ Global Scope

Variables declared outside of any function are in the global scope.

Accessible anywhere in the script.

📌 Example:

var globalVar = "I'm global";

function testScope() {

&nbsp;   console.log(globalVar); // ✅ Accessible inside function

}

testScope();

console.log(globalVar); // ✅ Accessible anywhere

2️⃣ Function Scope

Variables declared inside a function are only accessible within that function.

📌 Example:

function testFunctionScope() {

&nbsp;   var localVar = "I'm local";

}

console.log(localVar); // ❌ ReferenceError: localVar is not defined

3️⃣ Block Scope

Variables declared with let or const inside {} can’t be accessed outside.

📌 Example:

if (true) {

&nbsp;   let blockVar = "Inside block";

}

console.log(blockVar); // ❌ ReferenceError

✅ Only accessible inside {}.

Lexical Scope (Closure & Inheritance of Scope)

Lexical scope means a function can access variables from its parent scope, even after the parent function has finished executing.

📌 Example:

function outer() {

&nbsp;   let outerVar = "I'm from outer";

&nbsp;   function inner() {

&nbsp;       console.log(outerVar); // ✅ Inner function accesses outerVar

&nbsp;   }

&nbsp;   return inner;

}

const closureFunc = outer();

closureFunc(); // "I'm from outer" (Still remembers the variable!)

📝 Key Idea: Inner functions remember variables from where they were created, even if the outer function has finished execution.

\---------------------------------------------------------

\->Shadowing in JavaScript

Shadowing happens when a variable in a local scope (inside a function or block) has the same name as a variable in an outer scope (global or function scope). The inner variable "shadows" the outer one, meaning the outer variable is temporarily inaccessible within that scope.

🟢 Example of Shadowing

javascript

Copy

Edit

let x = "Global";

function example() {

&nbsp;   let x = "Local";  // Shadowing global \`x\`

&nbsp;   console.log(x);   // 👉 "Local" (local variable takes precedence)

}

example();

console.log(x);  // 👉 "Global" (global \`x\` remains unchanged)

🔹 Here, x inside example() shadows the global x. The inner x is used instead of the global x.

🟠 Shadowing with var, let, and const

Shadowing behaves differently depending on whether we use var, let, or const.

1️⃣ Shadowing with var (Function Scope)

javascript

Copy

Edit

var y = "Global var";

function testVarShadowing() {

&nbsp;   var y = "Local var";  // Shadows global \`y\`

&nbsp;   console.log(y);  // 👉 "Local var"

}

testVarShadowing();

console.log(y);  // 👉 "Global var"

✅ Allowed, because var is function-scoped.

2️⃣ Shadowing with let and const (Block Scope)

javascript

Copy

Edit

let z = "Global let";

if (true) {

&nbsp;   let z = "Block scoped let";  // Shadows global \`z\`

&nbsp;   console.log(z);  // 👉 "Block scoped let"

}

console.log(z);  // 👉 "Global let"

✅ Allowed, because let respects block scope.

🔴 Illegal Shadowing

If we shadow a variable declared with let or const using var in the same scope, it causes an error.

javascript

Copy

Edit

let a = "Global";

function testIllegalShadowing() {

&nbsp;   var a = "Local";  // ❌ SyntaxError: Identifier 'a' has already been declared

}

testIllegalShadowing();

❌ Illegal because var cannot shadow let or const in the same scope.

🟣 Shadowing in Nested Scopes

Shadowing can happen across multiple levels of scope.

javascript

Copy

Edit

let color = "Red";  // Global variable

function outer() {

&nbsp;   let color = "Blue";  // Shadows \`color\` from global scope

&nbsp;   function inner() {

&nbsp;       let color = "Green";  // Shadows \`color\` from outer function

&nbsp;       console.log(color);  // 👉 "Green"

&nbsp;   }

&nbsp;   inner();

&nbsp;   console.log(color);  // 👉 "Blue"

}

outer();

console.log(color);  // 👉 "Red"

✅ Each level has its own color variable, shadowing the outer scope.

🔹 Key Takeaways

Feature var let & const

Function Scope  ✅ Allowed   ✅ Allowed

Block Scope ❌ Not Block Scoped  ✅ Allowed

Shadowing in Different Scopes   ✅ Allowed   ✅ Allowed

Shadowing let/const with var    ❌ Causes Error  ❌ Causes Error