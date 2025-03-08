**1️⃣ Arithmetic Operators (+, -, \*, /, %, \*\*)**

Used for mathematical calculations.

| **Operator** | **Description**        | **Example** | **Output** |
|--------------|------------------------|-------------|------------|
| \+           | Addition               | 5 + 3       | 8          |
| \-           | Subtraction            | 5 - 3       | 2          |
| \*           | Multiplication         | 5 \* 3      | 15         |
| /            | Division               | 10 / 2      | 5          |
| %            | Modulus (Remainder)    | 10 % 3      | 1          |
| \*\*         | Exponentiation (Power) | 2 \*\* 3    | 8          |

**🔹 Example**

javascript

CopyEdit

console.log(5 + 3); // 8

console.log(10 % 3); // 1

console.log(2 \*\* 3); // 8

**2️⃣ Comparison Operators (==, ===, !=, !==, \>, \<, \>=, \<=)**

Used to compare two values.

| **Operator** | **Description**       | **Example** | **Output** |
|--------------|-----------------------|-------------|------------|
| ==           | Equal (loose)         | \"5\" == 5  | ✅ true    |
| ===          | Equal (strict)        | \"5\" === 5 | ❌ false   |
| !=           | Not equal (loose)     | \"5\" != 5  | ❌ false   |
| !==          | Not equal (strict)    | \"5\" !== 5 | ✅ true    |
| \>           | Greater than          | 10 \> 5     | ✅ true    |
| \<           | Less than             | 5 \< 10     | ✅ true    |
| \>=          | Greater than or equal | 10 \>= 10   | ✅ true    |
| \<=          | Less than or equal    | 5 \<= 10    | ✅ true    |

**🔹 Example**

javascript

CopyEdit

console.log(\"5\" == 5); // true (type coercion)

console.log(\"5\" === 5); // false (strict check)

console.log(10 \> 5); // true

**3️⃣ Logical Operators (&&, \|\|, !, ??)**

Used for boolean logic.

| **Operator** | **Description**    | **Example**         | **Output**  |
|--------------|--------------------|---------------------|-------------|
| &&           | AND                | true && false       | false       |
| \`           |                    | \`                  | OR          |
| !            | NOT                | !true               | false       |
| ??           | Nullish Coalescing | null ?? \"default\" | \"default\" |

**🔹 Example**

javascript

CopyEdit

console.log(true && false); // false

console.log(true \|\| false); // true

console.log(!true); // false

console.log(null ?? \"Hello\"); // \"Hello\"

**4️⃣ Bitwise Operators (&, \|, \^, \~, \<\<, \>\>, \>\>\>)**

Used for bitwise operations.

| **Operator** | **Description**       | **Example** | **Output** |
|--------------|-----------------------|-------------|------------|
| &            | AND                   | 5 & 3       | 1          |
| \`           | \`                    | OR          | \`5        |
| \^           | XOR                   | 5 \^ 3      | 6          |
| \~           | NOT                   | \~5         | -6         |
| \<\<         | Left shift            | 5 \<\< 1    | 10         |
| \>\>         | Right shift           | 5 \>\> 1    | 2          |
| \>\>\>       | Zero-fill right shift | -5 \>\>\> 1 | 2147483645 |

**🔹 Example**

javascript

CopyEdit

console.log(5 & 3); // 1 (0101 & 0011 = 0001)

console.log(5 \| 3); // 7 (0101 \| 0011 = 0111)

console.log(5 \^ 3); // 6 (0101 \^ 0011 = 0110)

console.log(\~5); // -6

**5️⃣ Assignment Operators (=, +=, -=, \*=, /=, %=, \*\*=)**

Used to assign values to variables.

| **Operator** | **Description**           | **Example** | **Equivalent to** |
|--------------|---------------------------|-------------|-------------------|
| =            | Assignment                | x = 10      | \-                |
| +=           | Add and assign            | x += 5      | x = x + 5         |
| -=           | Subtract and assign       | x -= 3      | x = x - 3         |
| \*=          | Multiply and assign       | x \*= 2     | x = x \* 2        |
| /=           | Divide and assign         | x /= 2      | x = x / 2         |
| %=           | Modulus and assign        | x %= 3      | x = x % 3         |
| \*\*=        | Exponentiation and assign | x \*\*= 2   | x = x \*\* 2      |

**🔹 Example**

javascript

CopyEdit

let x = 10;

x += 5; // x = x + 5 → 15

x \*= 2; // x = x \* 2 → 30

console.log(x);
