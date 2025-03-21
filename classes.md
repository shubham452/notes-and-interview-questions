**Classes (class, constructor, extends, super)**

- Modern syntax for creating objects in ES6.
- Supports inheritance with extends and super.
- Example: 

  class Animal {

  `  `constructor(name) {

  `    `this.name = name;

  `  `}

  `  `speak() {

  `    `return `${this.name} makes a sound`;

  `  `}

  }

  class Dog extends Animal {

  `  `speak() {

  `    `return `${this.name} barks`;

  `  `}

  }

  const dog = new Dog("Buddy");

  console.log(dog.speak()); // "Buddy barks"

