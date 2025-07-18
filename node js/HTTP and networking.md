## 4. HTTP and Networking in Node.js

Node.js provides robust capabilities for building servers, handling network communication, parsing URLs, and creating REST APIs. Here’s a guide with explanations and practical examples:

### **A. Creating an HTTP Server (Native `http` Module)**

- Use Node’s built-in `http` module; no external libraries required.
- The `http.createServer()` method creates a server and lets you handle incoming requests.

**Example: Basic HTTP Server**

```js
const http = require('http');

const server = http.createServer((req, res) => {
  res.writeHead(200, { 'Content-Type': 'text/plain' }); // Set response header
  res.end('Hello, World!'); // Send response body and finish response
});

server.listen(3000, () => {
  console.log('Server running at http://localhost:3000/');
});
```
- Visit `http://localhost:3000/` to see the server in action[1][2][3].

### **B. Handling Requests and Responses**

- The callback to `createServer()` receives two objects: `req` (request) and `res` (response).
- `req` contains HTTP method, URL, headers, and (optionally) incoming data.
- `res` allows you to set headers with `writeHead()`, write content with `write()`, and complete with `end()`.

**Example: Writing and Ending a Response**

```js
const server = http.createServer((req, res) => {
  res.write('Node.js powers backend networking!\n');
  res.end('Response complete.');
});
```
- Remember to always end the response with `res.end()` so the client receives a final reply[4].

### **C. URL Parsing and Query Strings**

Node.js makes it easy to work with URLs and query parameters:

- Use the built-in `url` and `querystring` modules, or the modern `URL` and `URLSearchParams` classes.

**Example 1: Parsing Query Strings with `querystring`**

```js
const querystring = require('querystring');

const urlQS = 'query=nodejs&sort=asc';
const params = querystring.parse(urlQS);
console.log(params); // { query: 'nodejs', sort: 'asc' }
```

**Example 2: Full URL Parsing**

```js
const { URL } = require('url');

const myURL = new URL('http://localhost:3000/search?term=node&lang=en');
console.log(myURL.search); // '?term=node&lang=en'
const params = new URLSearchParams(myURL.search);
console.log(params.get('term')); // 'node'
console.log(params.get('lang')); // 'en'
```
- These approaches help extract, process, and validate query parameters from user input[5][6][7].

### **D. Building REST APIs**

For REST APIs, it’s common to use frameworks like Express.js for simplicity and scalability, but you can create RESTful endpoints using only the native `http` module.

**Example: Minimal Native REST API**

```js
const http = require('http');
const { URL } = require('url');

const server = http.createServer((req, res) => {
  const parsedUrl = new URL(req.url, `http://${req.headers.host}`);
  
  if (req.method === 'GET' && parsedUrl.pathname === '/api/greet') {
    const name = parsedUrl.searchParams.get('name') || 'World';
    res.writeHead(200, { 'Content-Type': 'application/json' });
    res.end(JSON.stringify({ message: `Hello, ${name}!` }));
  } else {
    res.writeHead(404, { 'Content-Type': 'text/plain' });
    res.end('Not found');
  }
});

server.listen(3000, () => {
  console.log('REST API running at http://localhost:3000/');
});
```
- For more complex APIs, Express.js is a best practice, offering routing, middleware, and easier error handling[8][9][10].

### **Summary Table**

| Feature                    | Key Module/Concept              | Example Code                                  | Common Use                                     |
|----------------------------|----------------------------------|-----------------------------------------------|------------------------------------------------|
| HTTP Server                | `http` module                    | `http.createServer()`                         | Serving web or API requests                    |
| Handle Requests/Responses  | `req`, `res` objects             | `res.writeHead()`, `res.end()`                | Crafting custom responses                      |
| URL and Query String Parse | `url`, `querystring`, `URL`      | `URLSearchParams`, `querystring.parse()`      | Reading/searching URL params                   |
| REST APIs                  | Native or Express.js              | Custom routing and JSON responses             | Data-driven backends (CRUD, microservices)     |

**Interview Tips:**
- Know how to create a server and respond to every request.
- Practice parsing and validating URLs and query strings.
- Be prepared to build or explain simple REST API endpoints, both natively and with Express.

# REST API Best Practices: In-Depth Guide

Designing robust, scalable, and intuitive REST APIs requires more than just exposing endpoints—it involves thoughtful planning around resources, security, data structure, and maintainability. Below are best practices accepted by professionals and organizations to help you build high-quality RESTful APIs.

## 1. **Resource-Oriented URL Design**

- Use **nouns**, not verbs, for resource URLs.  
  - Good: `/users`, `/orders/123/items`
  - Bad: `/getUser`, `/createOrder`
- **Hierarchical endpoints** for relationships:  
  `/users/123/orders`
- Prefer **plural** nouns for collections: `/products`
- Use **unique IDs** to identify resources: `/articles/42`
- Avoid using file extensions in URLs (no `.json`/`.xml` in endpoints).

## 2. **HTTP Methods and Status Codes**

- Use the correct HTTP methods for actions:
  - `GET` – retrieve data (safe, idempotent)
  - `POST` – create resources (non-idempotent)
  - `PUT` – replace/update entire resource (idempotent)
  - `PATCH` – modify part of a resource (idempotent)
  - `DELETE` – remove a resource (idempotent)
- Respond with appropriate status codes:
  - `200 OK` (success, data exists)
  - `201 Created` (resource created)
  - `204 No Content` (successful delete or update with no return data)
  - `400 Bad Request` (invalid input)
  - `401 Unauthorized` / `403 Forbidden` (security issues)
  - `404 Not Found` (resource does not exist)
  - `409 Conflict` (resource conflict)
  - `500 Internal Server Error` (unexpected server error)

## 3. **Statelessness**

- Each API request should contain all information needed (authentication, data).
- The server should **not keep any user session state** between requests.
- Authentication is typically through stateless mechanisms such as JWT tokens or API keys.

## 4. **Consistent and Predictable Responses**

- Maintain a **consistent JSON structure** for responses.
  - Example:
    ```json
    {
      "data": { ... },
      "error": null,
      "meta": { ... }
    }
    ```
- Keys should follow a naming convention (`camelCase` or `snake_case`, but not both).
- Provide meaningful error responses:
    ```json
    {
      "error": {
        "code": 404,
        "message": "Resource not found"
      }
    }
    ```
- Always respond with a `Content-Type: application/json` header for JSON APIs.

## 5. **Filtering, Sorting, and Pagination**

- Support filtering via query strings:
  - `/users?role=admin`
- Allow sorting:
  - `/products?sort=price_asc`
- Implement pagination:
  - `/orders?page=2&limit=10`
  - Include pagination metadata in responses:
    ```json
    {
      "data": [...],
      "meta": {
        "total": 120,
        "page": 2,
        "limit": 10
      }
    }
    ```

## 6. **Versioning**

- Use URI versioning: `/v1/users`
- Never break clients by removing or changing fields in an existing API version.
- Document and deprecate old versions clearly before removal.

## 7. **Security Best Practices**

- **Enforce HTTPS** to encrypt data in transit.
- Require **authentication** for sensitive endpoints.
- Use **proper authorization** checks to enforce access control for different resources/operations.
- Rate-limit API requests to prevent abuse (e.g., with middleware like express-rate-limit).
- **Validate and sanitize** all input data to prevent injection or attacks.
- Do not leak implementation details or stack traces in error messages.
- Support CORS (Cross-Origin Resource Sharing) safely, restricting origins as needed.

## 8. **Documentation and Discoverability**

- Provide comprehensive, up-to-date API documentation (Swagger/OpenAPI, Postman collections).
- Document:
  - All endpoints, parameters, and return values
  - Authentication mechanisms
  - Common error responses and their meanings
- Example: Swagger UI lets consumers test endpoints interactively.

## 9. **HATEOAS (Hypermedia as the Engine of Application State)**

- Include hypermedia links in responses to guide clients through the API.
    ```json
    {
      "data": { "id": 123, "name": "Item" },
      "links": {
        "self": "/items/123",
        "owner": "/users/456"
      }
    }
    ```
- This makes APIs more navigable and self-documenting.

## 10. **Monitoring, Logging, and Error Handling**

- Log all requests, responses, and server errors securely (without sensitive data).
- Use tools like Winston, Morgan, or external monitoring (Datadog, Sentry).
- Implement centralized error-handling middleware (for example, in Express) to ensure all errors are managed uniformly.

## 11. **Data Validation and Type Safety**

- Validate input data on the server side (e.g., using Joi, Yup).
- Return clear validation errors to clients with contextual information.

## 12. **Idempotency and Safe HTTP Operations**

- Design `PUT`, `PATCH`, and `DELETE` endpoints so repeated calls with the same parameters do not adversely affect the system (“idempotent”).
- For `POST`, consider using idempotency keys for critical operations (e.g., payment APIs) to guard against duplicate processing.

## Best Practices Summary Table

| Practice              | Description                                                                    | Example/Tool                   |
|-----------------------|--------------------------------------------------------------------------------|-------------------------------|
| Resource Naming       | Plural nouns, hierarchical, no verbs                                          | `/users/42/orders`            |
| HTTP Method Use       | Match method to operation, correct status codes                               | `GET`, `POST`, `PUT`, etc.    |
| Statelessness         | No client state stored on server                                              | -                             |
| Consistent Responses  | Unified response/error shapes, clear `Content-Type`                           | JSON                          |
| Pagination & Filters  | Query params for paging/filtering                                             | `/posts?page=3&tag=nodejs`    |
| Versioning            | Do not break existing clients                                                 | `/v1/`                        |
| Secure by Default     | HTTPS, auth, rate-limiting, input validation                                  | JWT, express-rate-limit       |
| Documentation         | Self-explanatory, interactive documentation                                   | Swagger, OpenAPI              |
| Error Handling        | Robust, unambiguous responses, central middleware                             | Custom error objects          |
| Monitoring            | Logging, centralized error collection                                         | Winston, Sentry               |

