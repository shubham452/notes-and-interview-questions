# 8. Authentication and Security in Node.js

Secure Node.js backend development requires fundamental techniques and features for robust authentication and safe handling of sensitive data. This guide covers popular practices and code patterns for JWT/session-based authentication, password hashing with bcrypt, environment variables via dotenv, and Cross-Origin Resource Sharing (CORS).

## JWT (JSON Web Tokens) vs Session-Based Authentication

### **JWT Authentication**
- **JWTs** are self-contained tokens signed by the server and sent to the client after a successful login.
- On each request, the client sends the JWT (usually in an `Authorization` header).
- The server **verifies** the signature and extracts information (e.g., user ID) from the token, without storing session data server-side.
- **Stateless** and ideal for scalable APIs and microservices.

**Example Flow:**
1. User logs in → Server generates JWT → Sends it to client.
2. Client sends JWT in request headers for protected routes.
3. Server verifies token, processes request if valid.

**Use-case:** RESTful APIs, distributed/cloud-native systems.

### **Session-Based Authentication**
- Server creates a **session** with a unique session ID for each user after login.
- Session data is stored **server-side** (in-memory or in a database); the client gets only the session ID (typically in a cookie).
- On each request, the server uses this ID to retrieve session data.

**Use-case:** Traditional web apps, systems needing server-side session management, easier to invalidate user sessions.

| Feature                  | JWT (Token)         | Session-Based      |
|--------------------------|---------------------|--------------------|
| Storage                  | Client (token)      | Server (session)   |
| Scalability              | High                | Needs extra infra  |
| Stateless                | Yes                 | No                 |
| Revocation               | Challenging         | Simple             |

[1][2][3][4]

## Password Hashing (bcrypt)

- Never store plain-text passwords. Hash them securely before saving to the database.
- **bcrypt** is the industry standard for password hashing in Node.js.
    - Generates a **unique salt** for each password.
    - Repeatedly hashes the password + salt with a configurable "work factor," slowing brute-force attempts.
    - Hash and salt are stored (often as a single string); plain-text password is never saved.

**Installation:**
```bash
npm install bcrypt
```

**Hashing a Password:**
```js
const bcrypt = require('bcrypt');
const saltRounds = 10;

bcrypt.hash('user_password', saltRounds, (err, hash) => {
  // Save hash in DB
});
```

**Verifying a Password:**
```js
bcrypt.compare('input_password', storedHash, (err, result) => {
  if (result) {
    // Password matches
  } else {
    // Invalid password
  }
});
```


## Environment Variables (`dotenv`)

- Use environment variables to store secrets/configuration (e.g., DB credentials, API keys, JWT secrets) instead of hardcoding.
- The **dotenv** package loads environment variables from a `.env` file into `process.env`.

**Setup:**
1. Install package:
    ```bash
    npm install dotenv
    ```
2. Create a `.env` file:
    ```
    PORT=3000
    DATABASE_URL=mongodb://localhost:27017/mydb
    JWT_SECRET=supersecret
    ```
3. Load at the top of your main JS file:
    ```js
    require('dotenv').config();
    ```

**Access variables:**
```js
const port = process.env.PORT;
const dbUrl = process.env.DATABASE_URL;
const jwtSecret = process.env.JWT_SECRET;
```

*Never commit `.env` files to public repositories—add `.env` to your `.gitignore`!*

[5][6][7][8]

## Handling CORS

- **CORS** (Cross-Origin Resource Sharing) controls which web origins can access your server’s resources.
- Browsers block requests from origins not allowed by the server, unless proper CORS headers are set.
- For Express, use the `cors` middleware to configure allowed origins, methods, and headers.

**Setup:**
1. Install the CORS package:
    ```bash
    npm install cors
    ```
2. Usage in Express:
    ```js
    const express = require('express');
    const cors = require('cors');
    const app = express();

    // Allow all origins (not recommended for production)
    app.use(cors());

    // To restrict:
    const corsOptions = {
      origin: 'https://your-frontend.com'
    };
    app.use(cors(corsOptions));
    ```

**Apply CORS per route (optional):**
```js
app.get('/api/data', cors(corsOptions), (req, res) => {
  res.json({ msg: 'CORS-enabled endpoint' });
});
```


## Summary Table

| Security Feature     | Tool / Library   | Key Practice / Example         |
|--------------------- |------------------|-------------------------------|
| Token Authentication | JWT (`jsonwebtoken`) | Token in headers, stateless  |
| Session Auth         | express-session  | Server-managed, stateful      |
| Password Hashing     | bcrypt           | Salted hashes, never plain    |
| Env Variables        | dotenv           | `.env`, `process.env` access  |
| CORS                 | cors             | Whitelist origins, protect resources |

Follow these standards in any Node.js project to ensure your application is secure, configurable, and ready for production.
