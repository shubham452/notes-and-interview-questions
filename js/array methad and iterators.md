Here's a quick overview of Arrays and Iterables in JavaScript, covering
the methods and concepts you mentioned:

| **Topic**     | **Description**                                                            |
|---------------|----------------------------------------------------------------------------|
| **Arrays**    | Ordered collections of elements, indexed numerically.                      |
| **Iterables** | Objects that can be iterated using for\...of (like arrays, strings, sets). |

**Array Methods**

| **Method**    | **Description**                                             |
|---------------|-------------------------------------------------------------|
| map()         | Creates a new array by applying a function to each element. |
| filter()      | Creates a new array with elements that pass the test.       |
| reduce()      | Reduces array to a single value by applying a function.     |
| forEach()     | Executes a function on each element (no return value).      |
| some()        | Returns true if at least one element passes the test.       |
| every()       | Returns true if all elements pass the test.                 |
| find()        | Returns the first element that satisfies the condition.     |
| findIndex()   | Returns the index of the first matching element.            |
| indexOf()     | Returns the index of the first occurrence of a value.       |
| lastIndexOf() | Returns the last occurrence of a value.                     |
| push()        | Adds one or more elements to the end of the array.          |
| pop()         | Removes the last element and returns it.                    |
| shift()       | Removes the first element and returns it.                   |
| unshift()     | Adds one or more elements to the start of the array.        |
| splice()      | Adds/removes elements at a specific index.                  |
| sort()        | Sorts elements (default: lexicographical).                  |
| reverse()     | Reverses the order of elements.                             |
| slice()       | Returns a shallow copy of a portion of the array.           |
| flat()        | Flattens a nested array to the specified depth.             |
| flatMap()     | Maps each element and flattens the result.                  |
| join()        | Joins elements into a string with a specified separator.    |
| split()       | Splits a string into an array of substrings.                |

**Iterators and Generators**

| **Concept** | **Description**                                                      |
|-------------|----------------------------------------------------------------------|
| for\...of   | Iterates over iterable objects like arrays, strings, maps, and sets. |
| for\...in   | Iterates over enumerable properties of an object.                    |
| function\*  | Defines a generator function that can yield multiple values.         |
| yield       | Pauses the generator function and returns a value.                   |

**Set and WeakSet**

| **Concept** | **Description**                                                                  |
|-------------|----------------------------------------------------------------------------------|
| Set         | Collection of unique values.                                                     |
| WeakSet     | Similar to Set, but only stores objects and does not prevent garbage collection. |

**Map and WeakMap**

| **Concept** | **Description**                                                     |
|-------------|---------------------------------------------------------------------|
| Map         | Key-value pairs where keys can be of any type.                      |
| WeakMap     | Similar to Map, but keys must be objects and are weakly referenced. |

**Array Methods**

1.  **map()**

javascript

const numbers = \[1, 2, 3\];

const doubled = numbers.map(num =\> num \* 2);

console.log(doubled); // \[2, 4, 6\]

2.  **filter()**

javascript

const numbers = \[1, 2, 3, 4\];

const even = numbers.filter(num =\> num % 2 === 0);

console.log(even); // \[2, 4\]

3.  **reduce()**

javascript

const numbers = \[1, 2, 3, 4\];

const sum = numbers.reduce((acc, num) =\> acc + num, 0);

console.log(sum); // 10

4.  **forEach()**

javascript

const fruits = \[\'apple\', \'banana\', \'cherry\'\];

fruits.forEach(fruit =\> console.log(fruit));

5.  **some()**

javascript

const numbers = \[1, 2, 3\];

const hasEven = numbers.some(num =\> num % 2 === 0);

console.log(hasEven); // true

6.  **every()**

javascript

const numbers = \[2, 4, 6\];

const allEven = numbers.every(num =\> num % 2 === 0);

console.log(allEven); // true

7.  **find()**

javascript

const numbers = \[5, 12, 8, 130\];

const result = numbers.find(num =\> num \> 10);

console.log(result); // 12

8.  **findIndex()**

javascript

const numbers = \[5, 12, 8, 130\];

const index = numbers.findIndex(num =\> num \> 10);

console.log(index); // 1

9.  **indexOf()**

javascript

const fruits = \[\'apple\', \'banana\', \'cherry\'\];

console.log(fruits.indexOf(\'banana\')); // 1

10. **lastIndexOf()**

javascript

const numbers = \[2, 5, 9, 2\];

console.log(numbers.lastIndexOf(2)); // 3

11. **push()**

javascript

const arr = \[1, 2\];

arr.push(3);

console.log(arr); // \[1, 2, 3\]

12. **pop()**

javascript

const arr = \[1, 2, 3\];

arr.pop();

console.log(arr); // \[1, 2\]

13. **shift()**

javascript

const arr = \[1, 2, 3\];

arr.shift();

console.log(arr); // \[2, 3\]

14. **unshift()**

javascript

const arr = \[2, 3\];

arr.unshift(1);

console.log(arr); // \[1, 2, 3\]

15. **splice()**

javascript

const arr = \[1, 2, 3\];

arr.splice(1, 1, 4);

console.log(arr); // \[1, 4, 3\]

16. **sort()**

javascript

const fruits = \[\'banana\', \'apple\', \'cherry\'\];

fruits.sort();

console.log(fruits); // \[\'apple\', \'banana\', \'cherry\'\]

17. **reverse()**

javascript

const arr = \[1, 2, 3\];

arr.reverse();

console.log(arr); // \[3, 2, 1\]

18. **slice()**

javascript

const arr = \[1, 2, 3, 4\];

console.log(arr.slice(1, 3)); // \[2, 3\]

19. **flat()**

javascript

const arr = \[1, \[2, \[3, 4\]\]\];

console.log(arr.flat(2)); // \[1, 2, 3, 4\]

20. **flatMap()**

javascript

const arr = \[1, 2, 3\];

console.log(arr.flatMap(x =\> \[x, x \* 2\])); // \[1, 2, 2, 4, 3, 6\]

21. **join()**

javascript

const arr = \[\'Hello\', \'World\'\];

console.log(arr.join(\' \')); // \"Hello World\"

22. **split()**

javascript

const str = \'Hello World\';

console.log(str.split(\' \')); // \[\'Hello\', \'World\'\]

**Iterators and Generators**

23. **for\...of**

javascript

const arr = \[10, 20, 30\];

for (const num of arr) {

console.log(num);

}

// 10, 20, 30

24. **for\...in**

javascript

const obj = { a: 1, b: 2 };

for (const key in obj) {

console.log(key);

}

// a, b

25. **Generators**

javascript

function\* generator() {

yield 1;

yield 2;

yield 3;

}

const gen = generator();

console.log(gen.next().value); // 1

**Set and WeakSet**

26. **Set**

javascript

const set = new Set(\[1, 2, 3, 3\]);

console.log(set); // Set { 1, 2, 3 }

27. **WeakSet**

javascript

let obj1 = { a: 1 };

let obj2 = { b: 2 };

const weakSet = new WeakSet(\[obj1, obj2\]);

console.log(weakSet.has(obj1)); // true

**Map and WeakMap**

28. **Map**

javascript

const map = new Map();

map.set(\'name\', \'John\');

console.log(map.get(\'name\')); // John

29. **WeakMap**

javascript

let obj = { key: \'value\' };

const weakMap = new WeakMap();

weakMap.set(obj, 42);

console.log(weakMap.get(obj)); // 42
