**🚀 Memoization in JavaScript**

**🔹 What is Memoization?**

Memoization is an **optimization technique** that stores the results of
**expensive function calls** and returns the cached result when the same
inputs occur again.

📌 **Key Benefits:**  
✅ **Improves performance** by reducing redundant computations.  
✅ **Saves time** by reusing previous results.  
✅ **Useful for recursive functions**, like Fibonacci sequences.

**1️⃣ Basic Memoization Example**

Let\'s create a **simple memoization function** to cache results.

function memoize(fn) {

const cache = {};

return function (\...args) {

const key = JSON.stringify(args);

if (cache\[key\]) {

console.log(\"Fetching from cache:\", key);

return cache\[key\];

}

console.log(\"Computing result for:\", key);

const result = fn(\...args);

cache\[key\] = result;

return result;

};

}

// Example Function: Add Two Numbers

function add(a, b) {

return a + b;

}

// Memoized Version

const memoizedAdd = memoize(add);

console.log(memoizedAdd(2, 3)); // Computing result for: \[2,3\] → 5

console.log(memoizedAdd(2, 3)); // Fetching from cache: \[2,3\] → 5

console.log(memoizedAdd(4, 5)); // Computing result for: \[4,5\] → 9

🔹 **How it works:**

- If the function was called **before with the same arguments**, it
  **returns the cached result** instead of recomputing.

**4️⃣ Real-World Use Cases**

✅ **API Requests**  
Cache API responses to **avoid unnecessary network calls**.

const fetchWithCache = memoize(async function (url) {

const response = await fetch(url);

return response.json();

});

fetchWithCache(\"https://jsonplaceholder.typicode.com/todos/1\").then(console.log);

fetchWithCache(\"https://jsonplaceholder.typicode.com/todos/1\").then(console.log);
// Cached!

✅ **Expensive Calculations**  
Use memoization for **CPU-intensive computations**, like sorting large
datasets.

✅ **Form Validations**  
Prevent unnecessary re-validations in **React forms**.

**5️⃣ Summary**

✅ **Memoization caches function results** to speed up performance.  
✅ **Great for recursive functions** like Fibonacci and Factorial.  
✅ **Can be implemented using objects ({}) or Map for efficiency.**  
✅ **Useful in real-world scenarios** like API caching and expensive
computations.
