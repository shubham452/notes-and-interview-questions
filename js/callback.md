**Callbacks**

- A function passed as an argument to another function to be executed
  later.

- **Problem:** Can lead to \"Callback Hell\" when there are multiple
  nested callbacks.

**Example:**

function fetchData(callback) {

setTimeout(() =\> {

callback(\"Data loaded\");

}, 1000);

}

fetchData((message) =\> {

console.log(message); // Data loaded

});

**Callback Hell Example:**

setTimeout(() =\> {

console.log(\"Step 1\");

setTimeout(() =\> {

console.log(\"Step 2\");

setTimeout(() =\> {

console.log(\"Step 3\");

}, 1000);

}, 1000);

}, 1000);
