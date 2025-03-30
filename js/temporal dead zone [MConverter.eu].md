**Temporal Dead Zone (TDZ) in JavaScript**

The **Temporal Dead Zone (TDZ)** is the period between the **start of
execution** and the **point where a let or const variable is declared
and initialized**. During this time, accessing the variable **throws a
ReferenceError**.

**🟢 Example of Temporal Dead Zone**

javascript

CopyEdit

console.log(x); // ❌ ReferenceError: Cannot access \'x\' before
initialization

let x = 10;

console.log(x); // ✅ 10

🔹 **Why does this happen?**

- The variable x is **hoisted** to the top of the block, but it remains
  **uninitialized**.

- Until the let x = 10; line is executed, x is in the **TDZ**.

**🟠 Hoisting and TDZ**

Even though let and const are **hoisted** (moved to the top of their
scope), they remain **uninitialized** in the **TDZ**.

**🔹 var vs. let & const**

javascript

CopyEdit

console.log(a); // ✅ undefined (no TDZ for \`var\`)

var a = 5;

console.log(b); // ❌ ReferenceError (TDZ for \`let\`)

let b = 10;

✅ var variables are **hoisted and initialized** to undefined, so no
error occurs.  
❌ let and const variables are **hoisted but not initialized**, so
accessing them before declaration **throws an error**.

**🔴 TDZ with const**

Since const **must be initialized** when declared, it remains in the TDZ
until initialization.

javascript

CopyEdit

console.log(z); // ❌ ReferenceError

const z = 42;

**🟣 TDZ in if Blocks**

Variables declared inside an if block still enter the TDZ **until they
are initialized**.

javascript

CopyEdit

if (true) {

console.log(x); // ❌ ReferenceError (TDZ)

let x = \"Hello\";

console.log(x); // ✅ \"Hello\"

}

Even though the if condition is true, x is in the TDZ until it is
**declared and assigned**.

**🔹 TDZ in Function Parameters**

If a default function parameter uses a variable **declared later**, it
will throw a TDZ error.

javascript

CopyEdit

function example(a = b, b = 10) {

console.log(a, b);

}

example(); // ❌ ReferenceError: Cannot access \'b\' before
initialization

🔹 **b is in the TDZ when a tries to access it.**

**🚀 Key Takeaways**

| **Feature**                      | **var**                        | **let & const**                     |
|----------------------------------|--------------------------------|-------------------------------------|
| Hoisted?                         | ✅ Yes                         | ✅ Yes                              |
| Default Value Before Declaration | ✅ undefined                   | ❌ **No default value (TDZ error)** |
| Access Before Initialization     | ✅ Allowed (returns undefined) | ❌ **Throws ReferenceError (TDZ)**  |

**💡 Best Practices**

✔ Always declare let and const variables at the **top of their scope**
to avoid TDZ errors.  
✔ Understand that **variables exist in TDZ until their declaration is
reached**.  
✔ Use const for constants and let for variables that need reassignment.
