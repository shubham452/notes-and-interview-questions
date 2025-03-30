**Method Chaining**

- Calling multiple methods on the same object in a single statement.
- Example: 

  class Calculator {

  `  `constructor(value = 0) {

  `    `this.value = value;

  `  `}

  `  `add(num) {

  `    `this.value += num;

  `    `return this;

  `  `}

  `  `subtract(num) {

  `    `this.value -= num;

  `    `return this;

  `  `}

  }

  const result = new Calculator(10).add(5).subtract(3);

  console.log(result.value); // 12

