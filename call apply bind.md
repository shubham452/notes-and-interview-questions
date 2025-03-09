**🚀 call(), apply(), and bind() in JavaScript**

**📌 What are call(), apply(), and bind()?**

In JavaScript, **functions are objects**, which means they have methods.

- call(), apply(), and bind() are used to **control the this context** in functions.
- They allow **function borrowing**, enabling us to use methods from one object on another.
-----
**1️⃣ call() Method**

📌 **call() invokes a function immediately and allows passing arguments one by one.**

**Example: Using call()**

const person = {

`    `name: "Alice",

`    `greet: function (greeting) {

`        `console.log(`${greeting}, I am ${this.name}`);

`    `}

};

const person2 = { name: "Bob" };

person.greet.call(person2, "Hello"); // Output: Hello, I am Bob

🔹 **What happens here?**

- person.greet is originally for person, but we use call() to set this to person2.
- "Hello" is passed as a separate argument.
-----
**2️⃣ apply() Method**

📌 **apply() is similar to call(), but it takes arguments as an array.**

**Example: Using apply()**

const person = {

`    `name: "Alice",

`    `greet: function (greeting, punctuation) {

`        `console.log(`${greeting}, I am ${this.name}${punctuation}`);

`    `}

};

const person2 = { name: "Bob" };

person.greet.apply(person2, ["Hello", "!"]); // Output: Hello, I am Bob!

🔹 **What happens here?**

- apply() is like call(), but instead of individual arguments, it takes an **array**.
- Useful when you already have an **array of arguments**.
-----
**3️⃣ bind() Method**

📌 **bind() does NOT invoke the function immediately; instead, it returns a new function with this permanently set.**

**Example: Using bind()**

const person = {

`    `name: "Alice",

`    `greet: function (greeting) {

`        `console.log(`${greeting}, I am ${this.name}`);

`    `}

};

const person2 = { name: "Bob" };

const boundFunction = person.greet.bind(person2, "Hey");

boundFunction(); // Output: Hey, I am Bob

🔹 **What happens here?**

- bind() creates a **new function** where this is set to person2.
- The function is stored in boundFunction and **can be called later**.
-----
**4️⃣ Key Differences:**

|**Method**|**Calls Function Immediately?**|**Pass Arguments**|**Returns a New Function?**|
| :-: | :-: | :-: | :-: |
|call()|✅ Yes|**Individually**|❌ No|
|apply()|✅ Yes|**As an array**|❌ No|
|bind()|❌ No|**Individually**|✅ Yes|

-----
**5️⃣ Real-World Use Cases**

**✅ Function Borrowing**

Use call() or apply() to reuse methods from other objects.

const car = {

`    `brand: "Toyota",

`    `getInfo: function () {

`        `console.log(`This car is a ${this.brand}`);

`    `}

};

const bike = { brand: "Yamaha" };

car.getInfo.call(bike); // Output: This car is a Yamaha

**✅ Using apply() for Math Functions**

const numbers = [3, 1, 5, 8, 2];

console.log(Math.max.apply(null, numbers)); // Output: 8

console.log(Math.min.apply(null, numbers)); // Output: 1

🔹 **Why null?** Because Math.max() doesn’t rely on this, so we pass null.

**✅ Using bind() for Event Handlers**

In event listeners, bind() ensures the correct this context.

const button = document.querySelector("button");

const user = {

`    `name: "Alice",

`    `handleClick: function () {

`        `console.log(`Clicked by ${this.name}`);

`    `}

};

// Without bind, 'this' would refer to the button element

button.addEventListener("click", user.handleClick.bind(user));

🔹 **Why bind()?**

- Without bind(), this would refer to the button (<button>), not user.
-----
**🚀 Summary**

✅ call() → Calls function immediately, passes arguments **individually**.
✅ apply() → Calls function immediately, passes arguments **as an array**.
✅ bind() → **Does NOT call immediately**, but returns a **new function** with this set.

