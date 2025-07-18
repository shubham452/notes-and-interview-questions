## Node.js Modules and Packages: Explanations, Examples & Interview Questions

### 1. **CommonJS Modules (`require`, `module.exports`)**

**Explanation:**  
CommonJS is Node.js’s original module system. Every file is treated as a separate module. Use `require()` to import and `module.exports` (or `exports`) to export values.

**Example:**

- *module.js*
  ```js
  // math.js
  function add(a, b) { return a + b; }
  function subtract(a, b) { return a - b; }
  module.exports = { add, subtract };
  ```
- *main.js*
  ```js
  const math = require('./math');
  console.log(math.add(2, 3));      // 5
  console.log(math.subtract(7, 4)); // 3
  ```

**Interview Question:**  
Q: *How do you create and use a CommonJS module in Node.js?*  
A: Define code in a file, export what you want to share via `module.exports`, then import using `require('./filename')`[1][2].

### 2. **ES Modules (`import`, `export`)**

**Explanation:**  
ES Modules are the modern standard (native to browsers and Node.js >=12). Use `export`/`export default`, and import via `import`. You may need the `.mjs` extension or `"type": "module"` in `package.json`.

**Example:**

- *math.mjs*
  ```js
  export function add(a, b) { return a + b; }
  export function subtract(a, b) { return a - b; }
  ```
- *app.mjs*
  ```js
  import { add, subtract } from './math.mjs';
  console.log(add(5, 8));       // 13
  console.log(subtract(12, 7)); // 5
  ```

**Interview Question:**  
Q: *How are ES modules different from CommonJS?*  
A: ES modules use `import`/`export` syntax, support static analysis, and are the official JavaScript module standard, while CommonJS uses `require`/`module.exports` and loads modules dynamically. Node.js supports both, but ES modules may require extra setup[3][4].

### 3. **Node.js Core Modules**

**Explanation:**  
Node.js includes built-in modules—no install needed. Common examples:
- `fs`: File system operations  
- `http`: Create servers or handle HTTP  
- `path`: File and directory paths  
- `os`: System info  
- `url`: URL utilities

**Example:**

```js
const fs = require('fs');
fs.readFile('example.txt', 'utf8', (err, data) => {
  if (err) throw err;
  console.log(data);
});

const path = require('path');
console.log(path.basename('/foo/bar/baz.txt')); // baz.txt
```

**Interview Question:**  
Q: *How do you use Node.js core modules?*  
A: Require them directly, e.g., `const fs = require('fs');`. No need to install[5][6].

### 4. **npm: Installing, Updating, Removing Packages**

**Explanation:**  
npm (Node Package Manager) is used to manage third-party packages.

- **Install:**  
  ```
  npm install 
  ```
- **Update:**  
  ```
  npm update 
  ```
- **Remove/Uninstall:**  
  ```
  npm uninstall 
  ```

**Interview Question:**  
Q: *How do you remove a package with npm?*  
A: Run `npm uninstall ` in the project directory. For global packages, add `-g`, e.g., `npm uninstall -g `[7][8][9].

### 5. **Creating Your Own Modules**

**Explanation:**  
Write your functions, objects, or classes in a separate file and export them. Use `module.exports` for CommonJS or `export` for ES Modules.

**Example:**

- *calc.js (CommonJS)*
  ```js
  exports.add = (x, y) => x + y;
  exports.sub = (x, y) => x - y;
  ```
- *index.js (CommonJS)*
  ```js
  const calculator = require('./calc');
  console.log(calculator.add(10, 7)); // 17
  ```

**Interview Question:**  
Q: *Demonstrate how to create and use a custom module in Node.js.*  
A: Create a separate JS file, export functions/objects using `module.exports`, and import with `require('./filename')` in another file. For ES modules, use `export`/`import`[10][11].

## Quick Interview Table

| Topic                     | Example Code Snippet                           | Interview Key Point                                                    |
|---------------------------|------------------------------------------------|-----------------------------------------------------------------------|
| CommonJS Modules          | `const x = require('./mod')`                   | Classic Node.js modules; sync, widely compatible                      |
| ES Modules                | `import x from './mod.mjs'`                    | Modern, static analysis; use with `"type": "module"` or `.mjs`        |
| Core Modules              | `const fs = require('fs')`                     | Built-in libraries, no install needed                                 |
| npm Install/Remove        | `npm install lodash`, `npm uninstall lodash`   | Manages dependencies; `install`, `update`, `uninstall`                |
| Your Own Modules          | `exports.foo = ...` + `const x = require(...)` | Split code into files; export/import for reuse                        |

