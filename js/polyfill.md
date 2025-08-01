Absolutely! Here's your **full polyfill suite** with **testing code** and **line-by-line explanations** for every function.

---

### ✅ 1. `Array.prototype.myMap`

```javascript
Array.prototype.myMap = function (callback) {
  const temp = []; // create result array
  for (let i = 0; i < this.length; i++) {
    temp.push(callback(this[i], i, this)); // apply callback to each element
  }
  return temp; // return mapped array
};

// Test
console.log([1, 2, 3].myMap(x => x * 2)); // [2, 4, 6]
```

---

### ✅ 2. `Array.prototype.myFilter`

```javascript
Array.prototype.myFilter = function (callback) {
  const temp = [];
  for (let i = 0; i < this.length; i++) {
    if (callback(this[i], i, this)) temp.push(this[i]); // only if condition true
  }
  return temp;
};

// Test
console.log([1, 2, 3, 4].myFilter(x => x % 2 === 0)); // [2, 4]
```

---

### ✅ 3. `Array.prototype.myReduce`

```javascript
Array.prototype.myReduce = function (callback, initialValue) {
  let acc = initialValue; // start with given initial value
  let start = 0;
  if (acc === undefined) { // if no initialValue
    acc = this[0]; // use first element
    start = 1;
  }
  for (let i = start; i < this.length; i++) {
    acc = callback(acc, this[i], i, this); // accumulate result
  }
  return acc;
};

// Test
console.log([1, 2, 3, 4].myReduce((acc, val) => acc + val)); // 10
```

---

### ✅ 4. `Function.prototype.myCall`

```javascript
Function.prototype.myCall = function (context = {}, ...args) {
  if (typeof this !== 'function') throw new Error('Not callable');
  context.fn = this; // temporarily bind fn
  const result = context.fn(...args); // invoke
  delete context.fn; // clean up
  return result;
};

// Test
function greet(city) { return `${this.name} from ${city}`; }
console.log(greet.myCall({ name: 'Shubham' }, 'Delhi')); // Shubham from Delhi
```

---

### ✅ 5. `Function.prototype.myApply`

```javascript
Function.prototype.myApply = function (context = {}, argsArr = []) {
  if (typeof this !== 'function') throw new Error('Not callable');
  if (!Array.isArray(argsArr)) throw new Error('Args must be array');
  context.fn = this;
  const result = context.fn(...argsArr);
  delete context.fn;
  return result;
};

// Test
console.log(greet.myApply({ name: 'Shubham' }, ['Mumbai'])); // Shubham from Mumbai
```

---

### ✅ 6. `Function.prototype.myBind`

```javascript
Function.prototype.myBind = function (context = {}, ...args) {
  if (typeof this !== 'function') throw new Error('Not callable');
  const original = this; // store reference
  return function (...newArgs) {
    context.fn = original;
    const result = context.fn(...args, ...newArgs); // apply both arg sets
    delete context.fn;
    return result;
  };
};

// Test
const bound = greet.myBind({ name: 'Shubham' }, 'Bangalore');
console.log(bound()); // Shubham from Bangalore
```

---

### ✅ 7. `once`

```javascript
function once(func, context) {
  let ran;
  return function (...args) {
    if (func) {
      ran = func.apply(context || this, args); // run only once
      func = null; // clear function
    }
    return ran;
  };
}

// Test
const sayOnce = once((x) => console.log('Hi', x));
sayOnce('again'); // Hi again
sayOnce('again'); // no output
```

---

### ✅ 8. `myMemoize`

```javascript
function myMemoize(func, context) {
  const cache = {};
  return function (...args) {
    const key = JSON.stringify(args); // key based on arguments
    if (cache[key]) return cache[key]; // use cache
    cache[key] = func.call(context || this, ...args); // store result
    return cache[key];
  };
}

// Test
const fib = myMemoize(n => n <= 1 ? n : fib(n - 1) + fib(n - 2));
console.log(fib(10)); // 55
```

---

### ✅ 9. `PromisePolyfill`

```javascript
function PromisePolyfill(executor) {
  let onResolve, onReject;
  let isFulfilled = false;
  let isRejected = false;
  let isCalled = false;
  let value;

  function resolve(val) {
    isFulfilled = true;
    value = val;
    if (typeof onResolve === 'function' && !isCalled) {
      onResolve(val);
      isCalled = true;
    }
  }

  function reject(err) {
    isRejected = true;
    value = err;
    if (typeof onReject === 'function' && !isCalled) {
      onReject(err);
      isCalled = true;
    }
  }

  try {
    executor(resolve, reject); // execute with handlers
  } catch (e) {
    reject(e); // catch sync errors
  }

  this.then = function (cb) {
    onResolve = cb;
    if (isFulfilled && !isCalled) {
      onResolve(value);
      isCalled = true;
    }
    return this;
  };

  this.catch = function (cb) {
    onReject = cb;
    if (isRejected && !isCalled) {
      onReject(value);
      isCalled = true;
    }
    return this;
  };
}

// Test
new PromisePolyfill((res, rej) => res(42)).then(console.log); // 42
```

---

### ✅ 10. `Promise.resolve` and `Promise.reject`

```javascript
PromisePolyfill.resolve = function (val) {
  return new PromisePolyfill((res) => res(val));
};
PromisePolyfill.reject = function (val) {
  return new PromisePolyfill((_, rej) => rej(val));
};

// Test
PromisePolyfill.resolve('OK').then(console.log); // OK
PromisePolyfill.reject('Fail').catch(console.log); // Fail
```

---

### ✅ 11. `Promise.allPolyfill`

```javascript
Promise.allPolyfill = function (promises) {
  return new Promise((resolve, reject) => {
    const results = [];
    let pending = promises.length;
    if (pending === 0) return resolve(results);
    promises.forEach((p, idx) => {
      Promise.resolve(p)
        .then(res => {
          results[idx] = res;
          pending--;
          if (pending === 0) resolve(results);
        })
        .catch(reject); // any rejection causes all to reject
    });
  });
};

// Test
Promise.allPolyfill([
  Promise.resolve(1),
  Promise.resolve(2),
  Promise.resolve(3),
]).then(console.log); // [1, 2, 3]
```

---

### ✅ 12. `myDebounce`

```javascript
function myDebounce(callback, delay) {
  let timer;
  return function (...args) {
    clearTimeout(timer); // clear old timer
    timer = setTimeout(() => callback(...args), delay); // set new one
  };
}

// Test
const logDebounced = myDebounce(() => console.log('Debounced!'), 1000);
logDebounced(); logDebounced(); logDebounced(); // logs once after 1s
```

---

### ✅ 13. `myThrottle`

```javascript
function myThrottle(callback, delay) {
  let last = 0;
  return function (...args) {
    const now = Date.now();
    if (now - last < delay) return; // ignore if within delay
    last = now;
    callback(...args); // execute
  };
}

// Test
const logThrottled = myThrottle(() => console.log('Throttled!'), 1000);
setInterval(logThrottled, 200); // logs once every ~1s
```

---

Here are **simplified versions** of `slice` and `splice` polyfills that are beginner-friendly and still functionally correct for basic use cases:

---

## ✅ Simple `Array.prototype.slice` Polyfill

```javascript
Array.prototype.mySlice = function(start = 0, end = this.length) {
  const result = [];

  for (let i = start; i < end && i < this.length; i++) {
    if (i >= 0) result.push(this[i]);
  }

  return result;
};
```

### ▶ Example:

```javascript
const arr = [10, 20, 30, 40];
console.log(arr.mySlice(1, 3)); // [20, 30]
```

---

## ✅ Simple `Array.prototype.splice` Polyfill

```javascript
Array.prototype.mySplice = function(start, deleteCount, ...itemsToAdd) {
  const removed = [];

  // Remove items
  for (let i = start; i < start + deleteCount; i++) {
    removed.push(this[i]);
  }

  // Create new array with inserted items
  const left = this.slice(0, start);
  const right = this.slice(start + deleteCount);
  const newArr = left.concat(itemsToAdd, right);

  // Update original array
  this.length = 0;
  for (let i = 0; i < newArr.length; i++) {
    this.push(newArr[i]);
  }

  return removed;
};
```

### ▶ Example:

```javascript
const arr = [1, 2, 3, 4, 5];
const removed = arr.mySplice(2, 2, 99);
console.log(arr);      // [1, 2, 99, 5]
console.log(removed);  // [3, 4]
```

---

These versions skip handling edge cases like:

* negative indexes,
* large or missing `deleteCount`,
* sparse arrays.

Would you like a version that includes full edge case handling too?

