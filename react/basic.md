**✅ What is React, and why is it used?**

**React** is a JavaScript library for building **user interfaces**,
mainly for **single-page applications (SPAs)**.

-   It allows developers to create **reusable UI components**.

-   React is used because it’s **efficient**, **flexible**, and
    **declarative**.

**✅ What are the key features of React?**

-   **JSX** – JavaScript syntax extension to write HTML in JS.

-   **Component-Based** – UI is broken into reusable components.

-   **Virtual DOM** – Improves rendering performance.

-   **Unidirectional Data Flow** – Data flows from parent to child
    via props.

-   **Hooks** – Functional component capabilities (state, lifecycle).

-   **React Fiber** – Reconciler for async rendering.

**✅ What is JSX?**

**JSX (JavaScript XML)** is a syntax extension that allows writing
HTML-like code inside JavaScript.\
It gets compiled into React.createElement() calls.

jsx

const element = &lt;h1&gt;Hello&lt;/h1&gt;; // Transpiles to
React.createElement('h1', null, 'Hello')

**✅ What are components in React?**

Components are **reusable UI building blocks**.\
They can be:

-   **Functional Components** – Based on functions.

-   **Class Components** – Based on ES6 classes.

**✅ What is the difference between functional and class components?**

  **Feature**             **Functional Component**   **Class Component**
  ----------------------- -------------------------- ---------------------
  Syntax                  Function                   ES6 Class
  State                   useState Hook              this.state
  Lifecycle               useEffect, other hooks     Lifecycle methods
  Boilerplate             Less                       More
  Modern Recommendation   ✅ Preferred                Legacy

**✅ What is the virtual DOM, and how does it work?**

The **virtual DOM** is a lightweight JavaScript representation of the
real DOM.\
React uses it to:

1.  Create a virtual copy of the DOM.

2.  Compare it with the previous version (diffing).

3.  Update only the changed parts in the actual DOM (reconciliation).

**✅ Explain the concept of React Fiber.**

**React Fiber** is the **reconciliation engine** of React (since v16).\
It enables:

-   **Incremental rendering**

-   **Better interrupt handling** (e.g., pausing rendering for input)

-   **Priority-based updates**

Paste your rich text content here

**React Fiber** is the **reconciliation engine** in React — basically, it's the core of how React updates the UI. It was a complete rewrite of React’s rendering engine introduced in **React 16**.

  

### How React Fiber works (simple version):

Instead of rendering everything in one go, Fiber breaks work into **units**, then processes them **piece by piece**.

Imagine React is a painter. Before Fiber, the painter had to finish the entire painting in one go. Now, with Fiber, the painter can **pause**, check if there's a more urgent task, do that first, then continue the painting.

  

**✅ What are props in React?**

**Props (properties)** are **read-only data** passed from parent to
child components.\
They are used to configure components and make them reusable.

jsx

&lt;Greeting name="John" /&gt;

**✅ What is state in React?**

**State** is a **mutable** data structure used to manage data within a
component.\
It determines how the component renders and behaves.

jsx

const \[count, setCount\] = useState(0);

**✅ What is the difference between props and state?**

  **Feature**   **Props**               **State**
  ------------- ----------------------- --------------------------
  Mutability    Immutable (read-only)   Mutable (using hooks)
  Access        Passed from parent      Managed inside component
  Purpose       Configuration           Dynamic data/behavior

**✅ What is the significance of the key prop in lists?**

The key prop helps React **identify which items have changed, added, or
removed** in a list.\
It boosts **performance** during re-renders.

jsx

{items.map(item =&gt; &lt;li key={item.id}&gt;{item.name}&lt;/li&gt;)}

**✅ How do you handle events in React?**

React uses **camelCase** for event names and **JS functions** for
handlers.

&lt;button onClick={handleClick}&gt;Click me&lt;/button&gt;

You can pass parameters using arrow functions:

&lt;button onClick={() =&gt; handleClick(id)}&gt;Click&lt;/button&gt;

**✅ How does React render updates efficiently?**

-   Uses the **Virtual DOM** to detect changes.

-   Applies **diffing algorithm** to find minimal changes.

-   **Batches updates** to reduce reflows/repaints.

-   Uses **React Fiber** to break rendering into units of work.

**1. JSX Syntax**

-   **JSX** stands for **JavaScript XML**.

-   It allows writing HTML-like syntax inside JavaScript.

-   Transpiled to React.createElement() calls.

-   Example:

> jsx
>
> const element = &lt;h1&gt;Hello, world!&lt;/h1&gt;;

**2. Virtual DOM vs Real DOM**

  **Feature**    **Virtual DOM**                    **Real DOM**
  -------------- ---------------------------------- ----------------------
  Definition     Lightweight copy of the real DOM   Actual HTML DOM
  Speed          Faster updates                     Slower manipulation
  Updates        Batched and efficient              Direct and immediate
  Use in React   React uses it for performance      Browser renders it

**3. React Components (Function vs Class)**

  **Feature**      **Functional Component**      **Class Component**
  ---------------- ----------------------------- -----------------------
  Syntax           Function-based                ES6 class-based
  State Handling   useState, useEffect, etc.     this.state, lifecycle
  Performance      More lightweight and modern   Heavier and legacy
  Example                                        

jsx

function Hello() {

return &lt;h1&gt;Hello&lt;/h1&gt;;

}

jsx

class Hello extends React.Component {

render() {

return &lt;h1&gt;Hello&lt;/h1&gt;;

}

}

**4. Component Hierarchy & Tree**

-   Components are organized in a **tree-like structure**.

-   Parent components pass data to children via **props**.

-   Top-level component (usually &lt;App /&gt;) branches into children
    forming a tree.

**5. Reconciliation**

-   React’s **diffing algorithm** to update the DOM efficiently.

-   Compares previous and current virtual DOM trees.

-   Applies minimal set of changes to the real DOM.

**6. Keys in React**

-   Used in lists to uniquely identify elements.

-   Helps React in efficient reconciliation.

-   Must be **stable, unique, and not index** when possible.

-   Example:

> jsx
>
> items.map(item =&gt; &lt;li key={item.id}&gt;{item.name}&lt;/li&gt;);

**7. StrictMode**

-   A tool for **highlighting potential problems** in an app.

-   Wraps parts of your app to enforce best practices.

-   Only runs in development mode.

-   Example:

> jsx
>
> &lt;React.StrictMode&gt;
>
> &lt;App /&gt;
>
> &lt;/React.StrictMode&gt;
