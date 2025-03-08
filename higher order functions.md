**🔥 Higher-Order Functions in JavaScript**

**🚀 What is a Higher-Order Function?**

A **Higher-Order Function (HOF)** is a function that **either takes
another function as an argument or returns a function**. This concept is
fundamental in functional programming.

✅ **Key Features:**

1.  **Accepts a function** as an argument.

2.  **Returns a function** as a result.

3.  **Enhances code reusability** and modularity.

**1️⃣ Basic Example of a Higher-Order Function**

function greet(name, callback) {

console.log(\"Hello, \" + name + \"!\");

callback();

}

function sayGoodbye() {

console.log(\"Goodbye!\");

}

greet(\"Alice\", sayGoodbye);

// Output:

// Hello, Alice!

// Goodbye!

🔹 greet **accepts** sayGoodbye as a parameter, making it a
**higher-order function**.

**2️⃣ Common Built-in Higher-Order Functions**

JavaScript provides several built-in HOFs that simplify operations on
arrays.

**🔹 map() -- Transforming Data**

Creates a **new array** by applying a function to each element.

const numbers = \[1, 2, 3, 4\];

const squared = numbers.map(num =\> num \* num);

console.log(squared); // \[1, 4, 9, 16\]

**🔹 filter() -- Filtering Data**

Creates a **new array** with elements that pass a condition.

const ages = \[12, 18, 25, 30, 15\];

const adults = ages.filter(age =\> age \>= 18);

console.log(adults); // \[18, 25, 30\]

**🔹 reduce() -- Accumulate Values**

Reduces an array to a **single value**.

const nums = \[1, 2, 3, 4, 5\];

const sum = nums.reduce((acc, num) =\> acc + num, 0);

console.log(sum); // 15

**🔹 forEach() -- Iterating Over an Array**

Executes a function **for each element** in an array.

\const fruits = \[\"apple\", \"banana\", \"cherry\"\];

fruits.forEach(fruit =\> console.log(fruit));

// Output:

// apple

// banana

// cherry

**3️⃣ Writing Custom Higher-Order Functions**

You can create your own HOFs to make your code reusable and modular.

**🔹 Function that Returns Another Function**

function multiplyBy(factor) {

return function (num) {

return num \* factor;

};

}

const double = multiplyBy(2);

const triple = multiplyBy(3);

console.log(double(5)); // 10

console.log(triple(5)); // 15

🔹 multiplyBy(2) **returns a function** that multiplies by 2, making it
a **higher-order function**.

**🔹 Function that Accepts a Function as an Argument**

function applyOperation(a, b, operation) {

return operation(a, b);

}

function add(x, y) {

return x + y;

}

function subtract(x, y) {

return x - y;

}

console.log(applyOperation(10, 5, add)); // 15

console.log(applyOperation(10, 5, subtract)); // 5

🔹 applyOperation **accepts a function (add or subtract) as an
argument**, making it a **HOF**.

**4️⃣ Practical Uses of Higher-Order Functions**

**✅ Event Handling**

document.getElementById(\"btn\").addEventListener(\"click\", () =\> {

console.log(\"Button Clicked!\");

});

🔹 addEventListener **accepts a function as an argument**, making it a
**HOF**.

**✅ Debouncing & Throttling (Performance Optimization)**

Debouncing ensures a function is **executed after a delay** instead of
being called too frequently.

function debounce(func, delay) {

let timer;

return function (\...args) {

clearTimeout(timer);

timer = setTimeout(() =\> func(\...args), delay);

};

}

const handleSearch = debounce(() =\> console.log(\"Searching\...\"),
300);

document.getElementById(\"search\").addEventListener(\"input\",
handleSearch);

🔹 The debounce function **returns a new function**, making it a
**higher-order function**.

**5️⃣ Summary**

✅ **Higher-Order Functions (HOFs) can accept functions as arguments or
return functions.**  
✅ **They improve reusability, modularity, and code readability.**  
✅ **Common built-in HOFs include map(), filter(), reduce(), and
forEach().**  
✅ **They are widely used in event handling, functional programming, and
optimization techniques.**
