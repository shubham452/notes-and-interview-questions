**Getters & Setters (get, set)**

- Used to define custom behavior when accessing or modifying properties.
- Example: 

  class User {

  `  `constructor(name) {

  `    `this.\_name = name;

  `  `}

  `  `get name() {

  `    `return this.\_name.toUpperCase();

  `  `}

  `  `set name(newName) {

  `    `this.\_name = newName;

  `  `}

  }

  const user4 = new User("Emma");

  console.log(user4.name); // "EMMA"

  user4.name = "Sophia";

  console.log(user4.name); // "SOPHIA"

