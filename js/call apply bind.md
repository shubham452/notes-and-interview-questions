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

# Call, Apply, and Bind Interview Questions: Comprehensive Guide

## What are Call, Apply, and Bind?

Call, Apply, and Bind are three methods available on all JavaScript functions that allow you to explicitly set the `this` context and execute functions with different arguments. These methods enable **explicit binding** and **function borrowing** in JavaScript.[1][2]

### Key Differences

| Method | Execution | Arguments | Returns |
|--------|-----------|-----------|---------|
| **call()** | Immediate | Individual parameters | Function result |
| **apply()** | Immediate | Array of parameters | Function result |
| **bind()** | Delayed | Individual parameters | New bound function |

## Types of Interview Questions

### 1. Basic Conceptual Questions

#### Question: Explain the difference between call, apply, and bind

**Answer:**
- **call()**: Invokes function immediately with individual arguments[1]
- **apply()**: Invokes function immediately with arguments as an array[1]
- **bind()**: Returns a new function with bound context (doesn't execute immediately)[1]

```javascript
const person = { name: 'John' };

function greet(greeting, punctuation) {
    return `${greeting} ${this.name}${punctuation}`;
}

// call - individual arguments
console.log(greet.call(person, 'Hello', '!')); // "Hello John!"

// apply - array of arguments
console.log(greet.apply(person, ['Hi', '?'])); // "Hi John?"

// bind - returns new function
const greetJohn = greet.bind(person, 'Hey');
console.log(greetJohn('!!!')); // "Hey John!!!"
```

### 2. Output-Based Questions

#### Question 1: Predict the Output

```javascript
const person = { name: 'Piyush' };

function sayHi(age) {
    return `${this.name} is ${age} years old`;
}

console.log(sayHi.call(person, 24)); // ?
console.log(sayHi.bind(person, 24)); // ?
```

**Answer:**[3]
- First: `"Piyush is 24 years old"` (call executes immediately)
- Second: `function` (bind returns a function, doesn't execute)

#### Question 2: Complex Output Question

```javascript
const age = 10;
const person = {
    name: 'John',
    age: 20,
    getAge: function() {
        return this.age;
    }
};

const person2 = { age: 24 };
console.log(person.getAge.call(person2)); // ?
```

**Answer:** `24` (call changes `this` to person2)[3]

#### Question 3: Bind Chaining

```javascript
function f() {
    console.log(this.name);
}

const user = { name: 'John' };
const user2 = { name: 'Jane' };

f.bind(user).bind(user2)(); // What will this output?
```

**Answer:** `"John"` - **Bind chaining doesn't work**. Once a function is bound, it cannot be rebound.[4][3]

### 3. Advanced Coding Questions

#### Question 1: Fix the Broken Code

```javascript
const user = {
    firstName: 'John',
    sayHi() {
        console.log(`Hello, ${this.firstName}!`);
    }
};

setTimeout(user.sayHi, 1000); // This will print "Hello, undefined!"
```

**Solution using bind:**
```javascript
setTimeout(user.sayHi.bind(user), 1000); // "Hello, John!"
```

#### Question 2: Implement call() Polyfill

```javascript
Function.prototype.myCall = function(context = globalThis, ...args) {
    if (typeof this !== 'function') {
        throw new Error('Invalid function');
    }
    
    const fnKey = Symbol('fn');
    context[fnKey] = this;
    const result = context[fnKey](...args);
    delete context[fnKey];
    return result;
};

// Usage
function greet(greeting) {
    return `${greeting} ${this.name}`;
}

const person = { name: 'Alice' };
console.log(greet.myCall(person, 'Hello')); // "Hello Alice"
```

#### Question 3: Implement apply() Polyfill

```javascript
Function.prototype.myApply = function(context = globalThis, args = []) {
    if (typeof this !== 'function') {
        throw new Error('Invalid function');
    }
    
    const fnKey = Symbol('fn');
    context[fnKey] = this;
    const result = context[fnKey](...args);
    delete context[fnKey];
    return result;
};
```

#### Question 4: Implement bind() Polyfill

```javascript
Function.prototype.myBind = function(context = globalThis, ...args) {
    if (typeof this !== 'function') {
        throw new Error('Invalid function');
    }
    
    const fn = this;
    return function(...newArgs) {
        return fn.apply(context, [...args, ...newArgs]);
    };
};

// Usage
function multiply(a, b) {
    return a * b * this.factor;
}

const obj = { factor: 2 };
const multiplyByTwo = multiply.myBind(obj, 3);
console.log(multiplyByTwo(4)); // 24 (3 * 4 * 2)
```

### 4. Practical Application Questions

#### Question: Function Borrowing

```javascript
const person1 = {
    firstName: 'John',
    lastName: 'Doe',
    fullName: function() {
        return this.firstName + ' ' + this.lastName;
    }
};

const person2 = {
    firstName: 'Jane',
    lastName: 'Smith'
};

// How to use person1's fullName method for person2?
console.log(person1.fullName.call(person2)); // "Jane Smith"
console.log(person1.fullName.apply(person2)); // "Jane Smith"

const getFullName = person1.fullName.bind(person2);
console.log(getFullName()); // "Jane Smith"
```

#### Question: Array Method Borrowing

```javascript
// Convert NodeList to Array
const divs = document.querySelectorAll('div');
const divArray = Array.prototype.slice.call(divs);

// Or using apply
const divArray2 = Array.prototype.slice.apply(divs);

// Find max in array using apply
const numbers = [1, 5, 3, 9, 2];
const max = Math.max.apply(null, numbers); // 9
```

### 5. Arrow Functions and Binding

#### Question: Why doesn't call/apply/bind work with arrow functions?

```javascript
const obj = { num: 100 };
globalThis.num = 42;

// Regular function
function add(a, b, c) {
    return this.num + a + b + c;
}

// Arrow function
const addArrow = (a, b, c) => this.num + a + b + c;

console.log(add.call(obj, 1, 2, 3)); // 106
console.log(addArrow.call(obj, 1, 2, 3)); // 48 (uses globalThis.num)
```

**Answer:** Arrow functions don't have their own `this` binding. They inherit `this` from the surrounding lexical context.[5][6]

### 6. Edge Cases and Tricky Questions

#### Question 1: Null/Undefined Context

```javascript
function sayThis() {
    console.log(this);
}

sayThis.call(null); // In non-strict: window/global, In strict: null
sayThis.apply(undefined); // In non-strict: window/global, In strict: undefined
```

#### Question 2: Primitive Values as Context

```javascript
function showThis() {
    console.log(this);
    console.log(typeof this);
}

showThis.call('hello'); // String object, "object"
showThis.call(42); // Number object, "object"
showThis.call(true); // Boolean object, "object"
```

#### Question 3: Method Chaining with Bind

```javascript
const calculator = {
    value: 0,
    add: function(num) {
        this.value += num;
        return this;
    },
    multiply: function(num) {
        this.value *= num;
        return this;
    },
    getValue: function() {
        return this.value;
    }
};

// Create bound methods
const add = calculator.add.bind(calculator);
const multiply = calculator.multiply.bind(calculator);

// This won't work for chaining
// add(5).multiply(2); // Error: add returns calculator, but we called bound function

// Solution: Use call/apply or keep original context
calculator.add(5).multiply(2);
console.log(calculator.getValue()); // 10
```

### 7. Performance and Best Practices

#### Question: Performance comparison

**Performance ranking (fastest to slowest):**[7]
1. Direct function call
2. `call()` and `apply()`
3. `bind()` (creates new function)

```javascript
// Performance test example
const obj = { value: 10 };
function getValue() { return this.value; }

// Fastest
obj.getValue = getValue;
obj.getValue();

// Medium
getValue.call(obj);

// Slowest (due to function creation)
const boundGetValue = getValue.bind(obj);
boundGetValue();
```

## Common Interview Patterns

### Pattern 1: Context Loss and Solutions
- Event handlers losing context
- Callback functions in setTimeout/setInterval
- Method references passed as callbacks

### Pattern 2: Function Borrowing
- Array methods on array-like objects
- Math methods with arrays
- Object methods between different objects

### Pattern 3: Partial Application
- Creating specialized functions with preset arguments
- Currying implementations using bind
- Factory function patterns

### Pattern 4: Polyfill Implementation
- Understanding how call/apply/bind work internally
- Handling edge cases (null/undefined context)
- Symbol usage to avoid property conflicts

## Key Points to Remember

1. **Execution timing**: call/apply execute immediately, bind returns a function[1]
2. **Argument handling**: call takes individual args, apply takes array[2]
3. **Arrow functions**: Don't work with these methods due to lexical `this`[5]
4. **Bind chaining**: Doesn't work - functions can't be rebound[4]
5. **Polyfills**: Essential for understanding internal mechanics[8]
6. **Use cases**: Event handlers, callbacks, function borrowing, partial application[1]




