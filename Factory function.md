**Factory Functions**

- A function that returns an object.
- Used to create multiple similar objects.
- Example: 

  function createUser(name, age) {

  `  `return {

  `    `name,

  `    `age,

  `    `greet() {

  `      `return `Hello, ${name}`;

  `    `}

  `  `};

  }

  const user1 = createUser("Alice", 25);

  console.log(user1.greet()); // "Hello, Alice"

