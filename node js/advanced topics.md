# Node.js Advanced Topics: Explanations & Practical Examples

## Streams and Pipeline API

- **Streams** allow you to process data piece-by-piece, making them ideal for large files or real-time data. Node.js provides four types: Readable, Writable, Duplex, and Transform streams[1][2][3].
- The **pipeline API** (`stream.pipeline()`) connects multiple streams, handling errors and resource cleanup automatically. It simplifies tasks like file copying and compression.

**Example: Using pipeline to compress a file**
```js
const fs = require('fs');
const zlib = require('zlib');
const { pipeline } = require('stream');

pipeline(
  fs.createReadStream('input.txt'),
  zlib.createGzip(),
  fs.createWriteStream('input.txt.gz'),
  (err) => {
    if (err) console.error('Pipeline failed:', err);
    else console.log('Pipeline succeeded.');
  }
);
```
This code reads, compresses, and writes data efficiently[4][5].

## Worker Threads and Child Processes

- **Worker Threads** allow you to run JavaScript in multiple threads, suitable for CPU-bound tasks (e.g., image processing).
- **Child Processes** let you run separate processes, ideal for handling tasks in other languages or for process isolation.
- **Clusters** enable running multiple Node.js processes to distribute incoming connections across CPU cores[6][7][8].

**Example: Creating a worker thread**
```js
const { Worker } = require('worker_threads');
const worker = new Worker('./worker-script.js');
worker.on('message', msg => console.log('From worker:', msg));
worker.postMessage('start');
```
Use worker threads for computations and child_process for executing separate scripts or system commands.

## Performance Tuning and Profiling

- Use Node.js' built-in profiling tools (`--inspect`, `--prof`) and Chrome DevTools to find bottlenecks and memory leaks[9][10].
- Benchmark applications with tools like Autocannon or Artillery under simulated traffic.
- Regular profiling can reveal slow database queries, blocking code, or memory leaks, supporting targeted optimization.

**Profiling Command Example**
```bash
node --prof app.js
node --prof-process isolate-0x*.log > profile.txt
```

## Caching (Redis)

- Use **Redis** as a fast in-memory cache for frequently-requested data (e.g., API responses, session state), reducing API/database load[11][12].
- Integrate Redis with the `node-redis` package.
- Store responses in Redis after first fetch, and serve subsequent requests from cache.

**Example: Storing and retrieving data**
```js
const redis = require('redis');
const client = redis.createClient();
client.set('key', 'value');
client.get('key', (err, reply) => console.log(reply));
```
Caching improves speed and efficiency, especially for high-traffic endpoints.

## Rate Limiting

- Prevent abuse and control resource usage by placing caps on API requests per client within a specific time window[13][14].
- Common tools: `express-rate-limit` (for Express apps).

**Example: Rate limiting middleware**
```js
const rateLimit = require('express-rate-limit');
const limiter = rateLimit({
  windowMs: 15 * 60 * 1000, // 15 minutes
  max: 100, // limit per IP
  message: 'Too many requests, please try again later.'
});
app.use(limiter);
```

## WebSockets (Real-Time Applications)

- **WebSockets** enable two-way, always-on communication between client and server, supporting instant updates (chat apps, games, live dashboards)[15][16].
- Use `ws` or similar libraries to implement scalable, event-driven connections.

**Example: Basic WebSocket Server**
```js
const WebSocket = require('ws');
const wss = new WebSocket.Server({ port: 8080 });
wss.on('connection', ws => {
  ws.on('message', msg => ws.send(`Echo: ${msg}`));
});
```
Node.js is well-suited for real-time use cases due to its non-blocking, event-driven architecture.

## Building and Publishing npm Packages

1. **Create a package:** Write modular, reusable code.
2. **Initialize npm:** Run `npm init` to create a `package.json`.
3. **Build/test package:** Follow best practices for documentation, testing, and semantic versioning.
4. **Publish to npm:** Log in (`npm login`) and use `npm publish` to share the package on the npm registry. Scoped packages (e.g., `@username/package`) allow for organization-level management[17][18].

**Basic Steps**
```bash
npm init           # create package.json
npm adduser        # sign in to npm
npm publish        # upload to npm registry
```

## Summary Table

| Topic                           | Key Tool / Concept                | Practical Use                                  |
|----------------------------------|-----------------------------------|------------------------------------------------|
| Streams & pipeline               | `stream`, `pipeline()`            | Efficient data processing, file ops            |
| Worker threads & child_process   | `worker_threads`, `child_process` | Parallel tasks, CPU-intensive workloads        |
| Performance tuning/profiling     | `--inspect`, `--prof`, DevTools   | Optimize code, find bottlenecks                |
| Caching (Redis)                  | `redis`                           | Speed up APIs, offload databases               |
| Rate limiting                    | `express-rate-limit`              | Prevent abuse, improve reliability             |
| WebSockets                       | `ws`, `socket.io`                 | Build real-time web & mobile apps              |
| npm package publishing           | `npm init`, `npm publish`         | Share code, contribute to open source          |

Mastering these advanced Node.js topics equips you to build scalable, efficient, and secure modern applications.

