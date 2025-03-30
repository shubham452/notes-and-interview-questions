**Spread (\...) & Rest (\...) Operators**

Used for expanding or collecting elements.

| **Operator**  | **Description**             | **Example**           |
|---------------|-----------------------------|-----------------------|
| \... (Spread) | Expands elements            | \[\...arr\]           |
| \... (Rest)   | Collects remaining elements | function(\...args) {} |

**🔹 Example**

javascript

CopyEdit

// Spread (expanding)

const arr1 = \[1, 2, 3\];

const arr2 = \[\...arr1, 4, 5\];

console.log(arr2); // \[1, 2, 3, 4, 5\]

// Rest (collecting)

function sum(\...numbers) {

return numbers.reduce((a, b) =\> a + b, 0);

}

console.log(sum(1, 2, 3, 4)); // 10

**7️⃣ Nullish Coalescing (??)**

Returns the **right-hand** value if the **left-hand** value is null or
undefined.

| **Expression**           | **Output**  |
|--------------------------|-------------|
| null ?? \"default\"      | \"default\" |
| undefined ?? \"default\" | \"default\" |
| 0 ?? \"default\"         | 0           |
| \"\" ?? \"default\"      | \"\"        |

**🔹 Example**

javascript

CopyEdit

let name = null;

console.log(name ?? \"Guest\"); // \"Guest\"

**8️⃣ Optional Chaining (?.)**

Prevents errors when accessing properties of null or undefined.

| **Expression**  | **Output**                               |
|-----------------|------------------------------------------|
| obj?.prop       | undefined (if obj is null or undefined)  |
| obj?.method?.() | undefined (if obj.method doesn\'t exist) |

**🔹 Example**

javascript

CopyEdit

let user = { profile: { name: \"Alice\" } };

console.log(user?.profile?.name); // \"Alice\"

console.log(user?.address?.city); // undefined (no error)

**9️⃣ Destructuring Assignment**

Extracts values from arrays/objects.

| **Type**                 | **Example**                    |
|--------------------------|--------------------------------|
| **Array Destructuring**  | \[a, b\] = \[1, 2\]            |
| **Object Destructuring** | { name } = { name: \"Alice\" } |

**🔹 Example**

javascript

CopyEdit

// Array

const \[x, y\] = \[1, 2\];

console.log(x, y); // 1 2

// Object

const user = { name: \"Alice\", age: 25 };

const { name, age } = user;

console.log(name, age); // Alice 25

**🚀 Summary**

✅ Arithmetic (+, -, \*, /, %, \*\*)  
✅ Comparison (==, ===, !=, !==, \>, \<, \>=, \<=)  
✅ Logical (&&, \|\|, !, ??)  
✅ Bitwise (&, \|, \^, \~, \<\<, \>\>, \>\>\>)  
✅ Assignment (=, +=, -=, \*=, /=, %=, \*\*=)  
✅ **Advanced:** Spread, Rest, Nullish Coalescing, Optional Chaining,
Destructuring
