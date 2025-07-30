**Prototype inheritance** is a key concept in JavaScript and a few other programming languages, where objects can inherit properties and methods directly from other objects. This forms the basis for sharing behavior and code reuse, as opposed to class-based inheritance found in languages like Java or C++.

### How Prototype Inheritance Works

In JavaScript:
- Every object has an internal property called `[[Prototype]]` (accessible using `__proto__` in most environments).
- When you try to access a property or method on an object, and it doesn't exist on that object, JavaScript automatically looks for it on the object's prototype.
- This chain of searching for properties up the prototype chain is called the **prototype chain**.

### Example

```javascript
// Create a prototype object
const animal = {
  eats: true,
  walk() {
    console.log('Animal walks');
  }
};

// Create a new object inheriting from animal
const dog = Object.create(animal);
dog.bark = function() {
  console.log('Woof!');
};

console.log(dog.eats); // true (inherited from animal)
dog.walk();            // Animal walks (inherited from animal)
dog.bark();            // Woof! (dog's own method)
```

### Using Constructor Functions

```javascript
function Person(name) {
  this.name = name;
}
Person.prototype.greet = function() {
  console.log("Hello, " + this.name);
};

const alice = new Person("Alice");
alice.greet(); // Hello, Alice
```

### Key Points

- **Objects inherit from other objects** rather than from classes.
- Prototypes enable property/method sharing.
- You can set an object’s prototype using `Object.create`, `Object.setPrototypeOf`, or constructor functions with the `new` keyword.

### Why Use Prototype Inheritance?

- **Memory efficiency:** Shared methods are stored once on the prototype rather than on every object instance.
- **Dynamic sharing:** Modifying the prototype affects all inheriting objects.

If you want a deeper dive or have a specific question about prototype inheritance, feel free to ask!
