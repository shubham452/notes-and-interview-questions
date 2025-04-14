In React, **refs** (short for references) provide a way to access and
interact with DOM elements or React components directly. They allow you
to bypass the usual data flow (state and props) and can be useful for
things like focusing on an input element, measuring an element's size,
or triggering animations.

**Key Concepts of Refs:**

-   **useRef Hook**: In functional components, useRef is the main way to
    create a ref.

-   **createRef()**: In class components, you use createRef() to create
    a ref.

-   **Ref forwarding**: Refs can be passed to child components
    using React.forwardRef.

**Common Use Cases:**

1.  **Accessing a DOM Element**: This is the most common use of refs.

2.  **Storing Mutable Values**: Refs can be used to store values that
    don't trigger re-renders.

3.  **Triggering Animations**: Refs can be used to interact with
    third-party libraries for animations or to manually trigger
    DOM events.

**Example 1: Accessing a DOM Element with useRef**

In this example, a ref is used to focus on an input element when a
button is clicked.

**Code:**

jsx

import React, { useRef } from 'react';

function FocusInput() {

const inputRef = useRef(null);

const handleFocus = () =&gt; {

inputRef.current.focus(); // Focus the input element

};

return (

&lt;div&gt;

&lt;input ref={inputRef} type="text" placeholder="Click the button to
focus" /&gt;

&lt;button onClick={handleFocus}&gt;Focus Input&lt;/button&gt;

&lt;/div&gt;

);

}

export default FocusInput;

-   useRef(null) creates a reference to the input element.

-   The inputRef.current points to the DOM element, and focus() is
    called on it to give focus.

**Example 2: Storing Mutable Values with useRef**

Refs can also store mutable values that don't cause re-renders.

**Code:**

jsx

import React, { useState, useRef } from 'react';

function Timer() {

const \[seconds, setSeconds\] = useState(0);

const timerRef = useRef(null); // Mutable reference for timer ID

const startTimer = () =&gt; {

if (timerRef.current) return; // Prevent starting a new timer if one is
already running

timerRef.current = setInterval(() =&gt; {

setSeconds((prev) =&gt; prev + 1);

}, 1000);

};

const stopTimer = () =&gt; {

clearInterval(timerRef.current);

timerRef.current = null; // Reset ref after stopping

};

return (

&lt;div&gt;

&lt;p&gt;Seconds: {seconds}&lt;/p&gt;

&lt;button onClick={startTimer}&gt;Start Timer&lt;/button&gt;

&lt;button onClick={stopTimer}&gt;Stop Timer&lt;/button&gt;

&lt;/div&gt;

);

}

export default Timer;

-   The timerRef.current stores the setInterval ID, so it can be cleared
    when the timer is stopped.

**Example 3: Forwarding Refs to Child Components**

You can pass refs down to child components using React.forwardRef. This
is useful when you want to expose a ref from a parent component to a
child component, especially if the child is a custom component.

**Code:**

jsx

import React, { useRef } from 'react';

// Child component that forwards its ref

const CustomButton = React.forwardRef((props, ref) =&gt; (

&lt;button ref={ref} {...props}&gt;

{props.children}

&lt;/button&gt;

));

function App() {

const buttonRef = useRef(null);

const handleClick = () =&gt; {

alert(\`Button text is: \${buttonRef.current.textContent}\`);

};

return (

&lt;div&gt;

&lt;CustomButton ref={buttonRef} onClick={handleClick}&gt;

Click Me

&lt;/CustomButton&gt;

&lt;/div&gt;

);

}

export default App;

-   CustomButton forwards the ref to the &lt;button&gt; element
    using React.forwardRef.

-   In the parent App component, we can now use buttonRef to interact
    with the CustomButton's DOM element.

**Example 4: Accessing Class Components with Refs**

Refs can also be used to interact with **class components**.

**Code:**

jsx

import React, { useRef } from 'react';

class MyClassComponent extends React.Component {

focusInput = () =&gt; {

this.inputRef.focus();

};

render() {

return &lt;input ref={(ref) =&gt; (this.inputRef = ref)} /&gt;;

}

}

function App() {

const classComponentRef = useRef();

return (

&lt;div&gt;

&lt;MyClassComponent ref={classComponentRef} /&gt;

&lt;button onClick={() =&gt;
classComponentRef.current.focusInput()}&gt;Focus Input&lt;/button&gt;

&lt;/div&gt;

);

}

export default App;

-   We use ref to get access to the class component instance
    (MyClassComponent), allowing us to call methods like focusInput().

**Summary of Ref Usage:**

  **Use Case**                         **Example Code**
  ------------------------------------ --------------------------------------------------------------------
  **Accessing DOM Elements**           inputRef.current.focus() to focus an input element.
  **Storing Mutable Values**           Using useRef to store a setInterval ID or any mutable value.
  **Forwarding Refs to Child**         Passing refs to a custom child component using React.forwardRef.
  **Accessing Class Component Refs**   Using refs to access class component methods (e.g., focusInput()).

**Conclusion:**

-   **useRef** is a powerful hook that allows you to work with
    references to DOM elements and other mutable values.

-   **Forwarding refs** makes it easy to expose child components' refs
    to parent components.

-   Refs can be used in both **functional** and **class components**,
    and are typically employed when you need direct interaction with
    the DOM.
