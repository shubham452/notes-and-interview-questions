**🔹 use strict in JavaScript**

\"use strict\"; is a directive in JavaScript that enables **strict
mode**, which enforces a stricter set of rules to make JavaScript code
more secure, optimized, and less error-prone.

**🔹 How to Enable Strict Mode**

You can enable strict mode in **two ways**:

**1️⃣ Global Strict Mode**

Strict mode applies to the entire script if you put it at the top.

javascript

CopyEdit

\"use strict\";

x = 10; // ❌ ReferenceError: x is not defined

console.log(x);

✔ Without \"use strict\", JavaScript would **implicitly create** x as a
**global variable**.\
❌ With \"use strict\", JavaScript **prevents** this and throws an
error.

**2️⃣ Function-Level Strict Mode**

You can apply strict mode **only inside a function**.

javascript

CopyEdit

function myFunction() {

\"use strict\";

y = 20; // ❌ ReferenceError: y is not defined

}

myFunction();

✔ **Outside the function**, JavaScript behaves normally.\
❌ **Inside the function**, strict mode prevents accidental global
variable creation.

**🔹 Benefits of Strict Mode**

**1️⃣ Prevents Implicit Globals**

Without strict mode:

javascript

CopyEdit

x = 5; // No error, creates a global variable

console.log(x); // ✅ 5

With strict mode:

javascript

CopyEdit

\"use strict\";

x = 5; // ❌ ReferenceError: x is not defined

**2️⃣ Prevents Duplicate Parameter Names**

Without strict mode:

javascript

CopyEdit

function sum(a, a) { // No error (but bad practice)

return a + a;

}

console.log(sum(2, 3)); // ✅ 6 (last \`a\` is used)

With strict mode:

javascript

CopyEdit

\"use strict\";

function sum(a, a) { // ❌ SyntaxError: Duplicate parameter name not
allowed

return a + a;

}

**3️⃣ Prevents Deleting Variables and Functions**

Without strict mode:

javascript

CopyEdit

var a = 10;

delete a; // ❌ Fails silently, but no error

console.log(a); // ✅ 10

With strict mode:

javascript

CopyEdit

\"use strict\";

var a = 10;

delete a; // ❌ SyntaxError: Delete of an unqualified identifier in
strict mode

**4️⃣ Prevents Using Reserved Words**

Certain words are **reserved for future use** in JavaScript (e.g.,
interface, implements, public).

Without strict mode:

javascript

CopyEdit

var public = \"hello\"; // ✅ Works (but bad practice)

With strict mode:

javascript

CopyEdit

\"use strict\";

var public = \"hello\"; // ❌ SyntaxError: Unexpected strict mode
reserved word

**5️⃣ Prevents this from Defaulting to window**

Without strict mode:

javascript

CopyEdit

function showThis() {

console.log(this); // ✅ Window object

}

showThis();

With strict mode:

javascript

CopyEdit

\"use strict\";

function showThis() {

console.log(this); // ❌ undefined

}

showThis();

✔ Prevents unintended modifications to window.

**🔹 When to Use Strict Mode?**

✔ Always use \"use strict\"; at the **beginning of scripts or
functions**.\
✔ Helps catch common coding mistakes early.\
✔ Improves JavaScript performance by enabling optimizations.\
✔ Prevents bad practices like **implicit globals, duplicate parameters,
and reserved words usage**.

**🔹 Summary**

  -----------------------------------------------------------------------
  **Feature**            **Without \"use           **With \"use
                         strict\"**                strict\"**
  ---------------------- ------------------------- ----------------------
  Implicit globals       ✅ Allowed                ❌ ReferenceError

  Duplicate parameters   ✅ Allowed                ❌ SyntaxError

  Deleting variables     ✅ Fails silently         ❌ SyntaxError

  Reserved words         ✅ Allowed                ❌ SyntaxError

  this in functions      ✅ window                 ❌ undefined
  -----------------------------------------------------------------------
