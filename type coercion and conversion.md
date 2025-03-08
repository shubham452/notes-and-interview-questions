**3️⃣ Type Coercion (== vs ===)**

✔ JavaScript automatically converts types in **loose equality (==)** but
not in **strict equality (===)**.

| **Comparison** | **Result** | **Explanation**                |
|----------------|------------|--------------------------------|
| 5 == \"5\"     | ✅ true    | Loose equality (type coercion) |
| 5 === \"5\"    | ❌ false   | Strict equality (no coercion)  |
| 0 == false     | ✅ true    | false converts to 0            |
| 0 === false    | ❌ false   | Different types                |

**🔹 Example**

javascript

CopyEdit

console.log(5 == \"5\"); // true (coercion)

console.log(5 === \"5\"); // false (no coercion)

console.log(null == undefined); // true (both are \"empty\" values)

console.log(null === undefined); // false (different types)

**4️⃣ Implicit & Explicit Type Conversion**

**✅ Implicit Type Conversion (Type Coercion)**

JS automatically converts types when needed.

javascript

CopyEdit

console.log(\"5\" - 2); // 3 (string \"5\" → number 5)

console.log(\"5\" + 2); // \"52\" (number 2 → string \"2\")

console.log(\"10\" \* 2); // 20 (string \"10\" → number 10)

console.log(\"5\" - true); // 4 (true → 1)

console.log(\"5\" - null); // 5 (null → 0)

**✅ Explicit Type Conversion**

Using Number(), String(), Boolean(), etc.

javascript

CopyEdit

console.log(Number(\"42\")); // 42

console.log(String(42)); // \"42\"

console.log(Boolean(1)); // true

console.log(Boolean(0)); // false

console.log(Boolean(\"\")); // false (empty string)

console.log(Boolean(\"Hello\")); // true

**5️⃣ typeof, instanceof, isNaN, parseInt, parseFloat**

| **Method**     | **Purpose**                             | **Example**                   |
|----------------|-----------------------------------------|-------------------------------|
| **typeof**     | Returns type of a variable              | typeof \"hello\" → \"string\" |
| **instanceof** | Checks if an object belongs to a class  | arr instanceof Array → true   |
| **isNaN**      | Checks if a value is NaN (not a number) | isNaN(\"hello\") → true       |
| **parseInt**   | Converts string to an integer           | parseInt(\"42px\") → 42       |
| **parseFloat** | Converts string to a float              | parseFloat(\"3.14cm\") → 3.14 |

**🔹 Example**

javascript

CopyEdit

console.log(typeof 42); // \"number\"

console.log(typeof \"hello\"); // \"string\"

console.log(typeof true); // \"boolean\"

console.log(typeof {}); // \"object\"

console.log(typeof null); // \"object\" (historical JS bug)

console.log(typeof undefined); // \"undefined\"

let arr = \[1, 2, 3\];

console.log(arr instanceof Array); // true

console.log(arr instanceof Object); // true

console.log(isNaN(\"hello\")); // true

console.log(isNaN(42)); // false

console.log(isNaN(\"42\")); // false (auto-converts)

console.log(parseInt(\"42px\")); // 42

console.log(parseFloat(\"3.14cm\")); // 3.14

**🔹 Summary**

| **Concept**                  | **Description**                      | **Example**                                  |
|------------------------------|--------------------------------------|----------------------------------------------|
| **Primitive Types**          | Immutable data types stored by value | string, number, boolean, etc.                |
| **Reference Types**          | Mutable data stored by reference     | Object, Array, Function, etc.                |
| **Loose vs Strict Equality** | == allows type coercion, === doesn't | \"5\" == 5 (✅ true), \"5\" === 5 (❌ false) |
| **Implicit Type Conversion** | JS auto-converts types               | \"5\" - 2 → 3                                |
| **Explicit Type Conversion** | Using Number(), String(), etc.       | Number(\"42\") → 42                          |
| **typeof**                   | Returns type of a variable           | typeof \"hello\" → \"string\"                |
| **instanceof**               | Checks if object is of a type        | arr instanceof Array → true                  |
| **isNaN**                    | Checks if value is NaN               | isNaN(\"hello\") → true                      |
| **parseInt**                 | Converts string to integer           | parseInt(\"42px\") → 42                      |
| **parseFloat**               | Converts string to float             | parseFloat(\"3.14cm\") → 3.14                |
