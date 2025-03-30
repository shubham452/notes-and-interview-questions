**Object-Oriented JavaScript (OOP in JS)**

JavaScript is a prototype-based language that supports object-oriented
programming. Here are key concepts:

**Object Literals**

-   The simplest way to create an object.

-   Example:

> const person = {
>
> name: \"John\",
>
> age: 30,
>
> greet() {
>
> return \`Hello, my name is \${this.name}\`;
>
> }
>
> };
>
> console.log(person.greet()); // \"Hello, my name is John\"

**Object.create()**

-   Creates a new object using an existing object as a prototype.

-   Example:

> const personProto = { greet() { return \"Hello!\"; } };
>
> const user3 = Object.create(personProto);
>
> console.log(user3.greet()); // \"Hello!\"

**Object.assign(), Object.freeze(), Object.seal()**

-   **Object.assign(target, source)**: Copies properties from source to
    target.

> const obj1 = { a: 1 };
>
> const obj2 = { b: 2 };
>
> const obj3 = Object.assign({}, obj1, obj2);
>
> console.log(obj3); // { a: 1, b: 2 }

-   **Object.freeze(obj)**: Prevents adding, removing, or modifying
    properties.

> const obj4 = { a: 1 };
>
> Object.freeze(obj4);
>
> obj4.a = 2; // No effect
>
> console.log(obj4.a); // 1

-   **Object.seal(obj)**: Prevents adding/removing properties but allows
    modification.

> const obj5 = { a: 1 };
>
> Object.seal(obj5);
>
> obj5.a = 2; // Allowed
>
> delete obj5.a; // Not allowed
>
> console.log(obj5.a); // 2

**Object.entries(), Object.values(), Object.keys()**

-   **Object.keys(obj)**: Returns an array of object keys.

> const obj6 = { a: 1, b: 2 };
>
> console.log(Object.keys(obj6)); // \[\"a\", \"b\"\]

-   **Object.values(obj)**: Returns an array of object values.

> console.log(Object.values(obj6)); // \[1, 2\]

-   **Object.entries(obj)**: Returns an array of \[key, value\] pairs.

> console.log(Object.entries(obj6)); // \[\[\"a\", 1\], \[\"b\", 2\]\]
