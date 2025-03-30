**JavaScript Data Types**

JavaScript has **two** main categories of data types:\
✔ **Primitive types** (immutable, stored by value)\
✔ **Reference types** (mutable, stored by reference)

**1️⃣ Primitive Types**

Primitive types are **immutable** and stored **by value** (not by
reference).

  ---------------------------------------------------------------------------
  **Type**        **Example**            **Description**
  --------------- ---------------------- ------------------------------------
  **string**      \"Hello\"              Text enclosed in quotes

  **number**      42, 3.14               Integers & floating-point numbers

  **boolean**     true, false            Logical values

  **null**        null                   Intentional absence of value

  **undefined**   undefined              Default for uninitialized variables

  **bigint**      9007199254740991n      Large integers (use n at the end)

  **symbol**      Symbol(\'id\')         Unique and immutable values
  ---------------------------------------------------------------------------

**🔹 Example**

javascript

CopyEdit

let str = \"Hello\"; // string

let num = 42; // number

let isTrue = true; // boolean

let empty = null; // null

let notDefined; // undefined

let bigNum = 123n; // bigint

let sym = Symbol(\'id\'); // symbol

**2️⃣ Reference Types**

Reference types are **mutable** and stored **by reference** in memory.

  -------------------------------------------------------------------------
  **Type**       **Example**                 **Description**
  -------------- --------------------------- ------------------------------
  **Object**     { name: \"Alice\" }         Key-value pairs

  **Array**      \[1, 2, 3\]                 Ordered list of elements

  **Function**   function() {}               Block of reusable code

  **Date**       new Date()                  Represents date & time

  **RegExp**     /abc/                       Regular expressions
  -------------------------------------------------------------------------

**🔹 Example**

javascript

CopyEdit

let obj = { name: \"Alice\" }; // Object

let arr = \[1, 2, 3\]; // Array

function greet() { return \"Hello\"; } // Function

let date = new Date(); // Date object

let regex = /hello/; // Regular expression
