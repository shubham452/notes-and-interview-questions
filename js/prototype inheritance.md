**Prototype Inheritance**

-   Objects inherit properties/methods from their prototype.

-   Example:

> function Person(name) {
>
> this.name = name;
>
> }
>
> Person.prototype.greet = function() {
>
> return \`Hello, \${this.name}\`;
>
> };
>
> const user5 = new Person(\"Charlie\");
>
> console.log(user5.greet()); // \"Hello, Charlie\"

**\_\_proto\_\_ vs prototype**

  ------------------------------------------------------------------------------
  **Feature**   **\_\_proto\_\_**            **prototype**
  ------------- ---------------------------- -----------------------------------
  Type          Property of an object        Property of a function

  Purpose       Links object to its          Defines properties/methods for
                prototype                    future objects

  Usage         obj.\_\_proto\_\_            Function.prototype

  Example       obj.\_\_proto\_\_ ===        Constructor.prototype.method =
                Constructor.prototype        function() {\...}
  ------------------------------------------------------------------------------
