**5. Event Listeners**

| **Method**            | **Description**                           |
|-----------------------|-------------------------------------------|
| addEventListener()    | Attaches an event handler to an element.  |
| removeEventListener() | Removes an event handler from an element. |

**Example:**

function handleClick() {

alert(\"Button clicked!\");

}

const button = document.querySelector(\"#myButton\");

button.addEventListener(\"click\", handleClick);

// To remove the listener

button.removeEventListener(\"click\", handleClick);

**6. Event Delegation**

- Attaching a single event listener to a parent element to handle events
  from multiple children.

**Example:**

document.querySelector(\"#list\").addEventListener(\"click\", (e) =\> {

if (e.target.tagName === \"LI\") {

alert(\`Clicked on: \${e.target.textContent}\`);

}

});

**7. Event Propagation**

| **Type**  | **Description**                                           |
|-----------|-----------------------------------------------------------|
| Bubbling  | Event moves from the target element up through ancestors. |
| Capturing | Event moves from the root to the target element.          |

**Example:**

document.querySelector(\"#parent\").addEventListener(\"click\", () =\> {

console.log(\"Parent clicked\");

}, true); // Capturing

document.querySelector(\"#child\").addEventListener(\"click\", () =\> {

console.log(\"Child clicked\");

}); // Bubbling

**8. Controlling Event Propagation**

| **Method**        | **Description**                           |
|-------------------|-------------------------------------------|
| stopPropagation() | Stops the event from bubbling/capturing.  |
| preventDefault()  | Prevents the default action of the event. |

**Example:**

const link = document.querySelector(\"a\");

link.addEventListener(\"click\", (e) =\> {

e.preventDefault(); // Stops link navigation

alert(\"Link click prevented\");

});

document.querySelector(\"#inner\").addEventListener(\"click\", (e) =\> {

e.stopPropagation(); // Stops bubbling

alert(\"Inner clicked\");

});

**9. MutationObserver API**

- Watches for changes in the DOM tree.

**Example:**

const targetNode = document.querySelector(\"#observed\");

const observer = new MutationObserver((mutations) =\> {

mutations.forEach((mutation) =\> {

console.log(\"Mutation detected:\", mutation);

});

});

observer.observe(targetNode, { childList: true, subtree: true });

// To test: Dynamically add a child

targetNode.appendChild(document.createElement(\"p\"));
