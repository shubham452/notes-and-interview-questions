# 9. Error Handling and Debugging in Node.js

## Try-Catch and Error Middleware

### Try-Catch
- In **synchronous code** and within `async` functions, use `try-catch` to manage errors.
- Place suspicious code inside the `try` block; handle errors in `catch`.

**Example (async/await):**
```js
async function readFileData(path) {
  try {
    const data = await fs.promises.readFile(path, 'utf8');
    console.log('File content:', data);
  } catch (err) {
    console.error('Error reading file:', err.message);
  }
}
```

### Express Error Middleware
- In **Express.js**, custom error-handling middleware lets you catch and respond to errors in routes and middleware.
- Declare error middleware with four arguments: `(err, req, res, next)`.

**Example:**
```js
app.use((err, req, res, next) => {
  console.error('Error:', err.stack);
  res.status(500).json({ error: 'Something went wrong!' });
});
```
- Use `next(err)` in routes/middleware to route errors to this handler.

## Console Logging and Debugging Tools

### Console Logging
- Use `console.log()`, `console.info()`, `console.warn()`, and `console.error()` to output debugging and status info.
- For structured data, use `console.dir(obj, { depth: null })`.

**Example:**
```js
console.log('Starting server...');
console.error('Validation error:', err);
```

### Advanced Debugging Tools
- **Debugger Statement**: Insert `debugger;` in code to set breakpoints.
- **Logging Libraries**: Use `winston`, `morgan`, or similar for more control, formatting, or persistent logs.

**Example:** Use `winston` for advanced file and console logs.
```js
const winston = require('winston');
const logger = winston.createLogger({ /* ...options... */ });
logger.error('This is an error message');
```

## Using Node.js Inspector

- Node.js provides a built-in debugger accessible by running your script with the `inspect` flag.

### How to Use the Inspector
1. Start Node.js with inspector:
   ```
   node --inspect app.js
   ```
2. Open `chrome://inspect` in Chrome and connect to your running process.
3. Set breakpoints, step through code, and examine variables in real time.
4. You can also use Visual Studio Code’s integrated debugger for Node.js.

### Quick Usage Example
- To start in break mode (pause on first line):
  ```
  node --inspect-brk app.js
  ```
- When running, add `debugger;` statements to force the inspector to pause at certain points.

## Summary Table

| Feature                | Purpose                             | Example/Usage                                |
|------------------------|-------------------------------------|----------------------------------------------|
| Try-Catch              | Handle sync/async errors            | `try { ... } catch (e) { ... }`              |
| Express Error Middleware| Central error handling in web apps  | `app.use((err, req, res, next) => {...})`    |
| Console Logging        | Output status/error/debug info      | `console.log()`, `console.error()`           |
| Logging Libraries      | Advanced logging and monitoring     | `winston`, `morgan`                          |
| Node Inspector         | Step-through debugging in Node.js   | `node --inspect app.js` + browser/IDE tools  |

### Interview Insights
- Always validate and handle errors close to where they may occur.
- Segregate logging and error handling logic from core business logic.
- Leverage built-in and external debugging tools for robust troubleshooting in production and development.
