**2. Promises**

- Objects representing the eventual completion or failure of an
  asynchronous operation.

| **Method** | **Description**                         |
|------------|-----------------------------------------|
| resolve()  | Successfully complete the promise.      |
| reject()   | Mark the promise as failed.             |
| then()     | Runs when the promise is resolved.      |
| catch()    | Runs when the promise is rejected.      |
| finally()  | Runs regardless of the promise outcome. |

**Creating a Promise:**

const myPromise = new Promise((resolve, reject) =\> {

const success = true;

if (success) {

resolve(\"Operation Successful\");

} else {

reject(\"Operation Failed\");

}

});

myPromise

.then((message) =\> console.log(message))

.catch((error) =\> console.log(error))

.finally(() =\> console.log(\"Done\"));

**3. Promise Chaining**

- Chaining multiple .then() for sequential asynchronous operations.

**Example:**

new Promise((resolve) =\> resolve(1))

.then((result) =\> result \* 2)

.then((result) =\> result \* 3)

.then((result) =\> console.log(result)); // 6

**4. Promise Methods**

| **Method**           | **Description**                                                |
|----------------------|----------------------------------------------------------------|
| Promise.all()        | Resolves when all promises resolve, rejects if any fail.       |
| Promise.race()       | Resolves or rejects as soon as one of the promises settles.    |
| Promise.allSettled() | Returns results of all promises, whether resolved or rejected. |
| Promise.any()        | Resolves as soon as one promise resolves (ignores rejections). |

**Examples:**

const p1 = Promise.resolve(\"Success\");

const p2 = Promise.reject(\"Error\");

const p3 = Promise.resolve(\"Another Success\");

Promise.all(\[p1, p3\]).then(console.log); // \[\"Success\", \"Another
Success\"\]

Promise.race(\[p1, p3\]).then(console.log); // \"Success\"

Promise.allSettled(\[p1, p2, p3\]).then(console.log);

// \[{status: \"fulfilled\", value: \"Success\"}, {status: \"rejected\",
reason: \"Error\"}, {status: \"fulfilled\", value: \"Another
Success\"}\]

Promise.any(\[p2, p3\]).then(console.log); // \"Another Success\"

**5. Async/Await**

- A syntactic sugar over Promises to make asynchronous code look
  synchronous.

- Works with functions marked as async.

**Example:**

async function fetchData() {

try {

const response = await new Promise((resolve) =\>

setTimeout(() =\> resolve(\"Data fetched\"), 1000)

);

console.log(response); // Data fetched

} catch (error) {

console.error(error);

}

}

fetchData();

**6. Error Handling with try\...catch in Async Functions**

- Used to catch errors from asynchronous operations.

**Example:**

async function fetchData() {

try {

throw new Error(\"Something went wrong\");

} catch (error) {

console.error(\"Error:\", error.message); // Error: Something went wrong

}

}

fetchData();
