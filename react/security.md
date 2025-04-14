**🔐 1. Avoid dangerouslySetInnerHTML (Unless Sanitized)**

-   This opens the door to **XSS attacks**.

-   If absolutely needed (e.g., rendering HTML from CMS), use a
    **sanitizer** like DOMPurify.

jsx

import DOMPurify from 'dompurify';

&lt;div dangerouslySetInnerHTML={{ \_\_html:
DOMPurify.sanitize(userInput) }} /&gt;

**🛡 2. Prevent XSS in Props**

-   React **escapes all props by default**, which protects against XSS.

-   BUT: don’t inject raw HTML or user-controlled content
    using dangerouslySetInnerHTML.

**✅ Safe:**

jsx

&lt;p&gt;{userInput}&lt;/p&gt; // React escapes this safely

**❌ Risky:**

jsx

&lt;p dangerouslySetInnerHTML={{ \_\_html: userInput }} /&gt; //
vulnerable

**🌐 3. Use HTTPS APIs**

-   Always fetch data from secure https:// endpoints.

-   Helps protect data in transit and avoids mixed content issues
    in browsers.

jsx

const res = await fetch('https://api.example.com/data');

**🔑 4. JWT Handling (Prefer HttpOnly Cookies)**

  **Option**             **Pros**                        **Cons**
  ---------------------- ------------------------------- -----------------------------
  **HttpOnly Cookie**    Immune to XSS, secure storage   Needs backend to set cookie
  localStorage/session   Easy to use, frontend-only      Vulnerable to XSS

**Recommended:**

-   Store JWT in an **HttpOnly cookie** (set by server).

-   Backend reads it on each request automatically.

**🔐 5. Protect Routes & Auth Checks**

-   Add logic to block access to protected pages for
    unauthenticated users.

**Example:**

jsx

const PrivateRoute = ({ children }) =&gt; {

const isAuth = Boolean(localStorage.getItem('token')); // or use
context/auth state

return isAuth ? children : &lt;Navigate to="/login" /&gt;;

};

jsx

&lt;Route path="/dashboard" element={&lt;PrivateRoute&gt;&lt;Dashboard
/&gt;&lt;/PrivateRoute&gt;} /&gt;

Also validate the token **on the server**.

**🌍 6. CORS Configuration in Development**

-   Set up **CORS** on the backend (Access-Control-Allow-Origin) to
    allow requests from frontend during development.

**Example (Express.js):**

js

app.use(cors({

origin: 'http://localhost:3000',

credentials: true // for cookies/auth headers

}));

Avoid "\*" for origin in production. Always **whitelist trusted
domains**.

**✅ Summary**

  **Practice**                       **Why It Matters**
  ---------------------------------- --------------------------------------
  Avoid dangerouslySetInnerHTML      Prevents XSS
  React props auto-escape            Safe rendering of user input
  Use HTTPS                          Secure communication
  JWT in HttpOnly cookies            Prevent token theft via XSS
  Route protection + server checks   Prevents unauthorized access
  Secure CORS settings               Enables cross-origin requests safely
