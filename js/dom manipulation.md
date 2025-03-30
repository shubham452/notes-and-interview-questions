**1. Selecting Elements**

| **Method**                | **Description**                     |
|---------------------------|-------------------------------------|
| document.querySelector()  | Selects the first matching element. |
| document.getElementById() | Selects an element by its ID.       |

**Example:**

const para = document.querySelector(\".my-class\");

const header = document.getElementById(\"main-header\");

console.log(para, header);

**2. Modifying Content**

| **Property** | **Description**                            |
|--------------|--------------------------------------------|
| innerHTML    | Sets/gets the HTML content of an element.  |
| textContent  | Sets/gets the text content (ignores HTML). |

**Example:**

const div = document.querySelector(\"#content\");

div.innerHTML = \"\<p\>Hello, World!\</p\>\"; // Adds HTML

div.textContent = \"Just Text\"; // Replaces with plain text

**3. Adding and Removing Elements**

| **Method**    | **Description**                               |
|---------------|-----------------------------------------------|
| appendChild() | Adds a node to the end of a list of children. |
| removeChild() | Removes a specified child node.               |

**Example:**

const list = document.querySelector(\"#myList\");

const newItem = document.createElement(\"li\");

newItem.textContent = \"New Item\";

list.appendChild(newItem); // Add item

list.removeChild(newItem); // Remove item

**4. Managing Classes**

| **Method**         | **Description**                  |
|--------------------|----------------------------------|
| classList.add()    | Adds a class to an element.      |
| classList.remove() | Removes a class from an element. |

**Example:**

const box = document.querySelector(\".box\");

box.classList.add(\"active\"); // Add class

box.classList.remove(\"hidden\"); // Remove class
