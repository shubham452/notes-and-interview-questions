**1. Same-Origin Policy (SOP)**

- Restricts how documents/scripts from one origin can interact with
  resources from another origin.

- Origin = Protocol + Domain + Port

**Example:**

- A script loaded from https://example.com cannot make a request to
  https://another.com.

- Browsers block cross-origin requests unless explicitly allowed (e.g.,
  via CORS).

**2. Cross-Origin Resource Sharing (CORS)**

- Allows servers to specify who can access their resources.

- Uses HTTP headers to control access.

**Example:**  
In Express.js:

const express = require(\"express\");

const cors = require(\"cors\");

const app = express();

app.use(cors()); // Allow all origins

app.get(\"/data\", (req, res) =\> {

res.json({ message: \"Hello, CORS!\" });

});

app.listen(3000, () =\> console.log(\"Server running on port 3000\"));

**CORS Headers:**

- Access-Control-Allow-Origin: Specifies allowed origin.

- Access-Control-Allow-Methods: Specifies allowed HTTP methods.

- Access-Control-Allow-Headers: Specifies allowed request headers.

**3. Content Security Policy (CSP)**

- Mitigates XSS by controlling the resources the browser is allowed to
  load.

**Example:**

\<meta http-equiv=\"Content-Security-Policy\" content=\"default-src
\'self\'; script-src \'self\' https://trustedscripts.com;\"\>

- Restricts scripts to load only from the same origin and from
  https://trustedscripts.com.

- Helps prevent malicious script injections.

**4. JSON Web Tokens (JWT)**

- Used for securely transmitting information between parties.

- Consists of Header, Payload, and Signature.

**Example:**  
Generating a JWT in Node.js:

javascript

CopyEdit

const jwt = require(\"jsonwebtoken\");

const token = jwt.sign({ userId: 123 }, \"secretKey\", { expiresIn:
\"1h\" });

console.log(\"JWT:\", token);

**Verification:**

try {

const decoded = jwt.verify(token, \"secretKey\");

console.log(\"Decoded:\", decoded);

} catch (error) {

console.log(\"Invalid token\");

}

**Best Practice:** Store JWT in httpOnly cookies for added security.

**5. XSS (Cross-Site Scripting) Prevention**

- Attackers inject malicious scripts into trusted websites.

**Prevention Methods:**

| **Technique**           | **Description**                        |
|-------------------------|----------------------------------------|
| Input Validation        | Sanitize and validate user inputs.     |
| Escaping Output         | Use libraries to escape HTML, CSS, JS. |
| Content Security Policy | Restrict script sources using CSP.     |

**Example:**

// Example of sanitizing user input

const sanitize = (input) =\> input.replace(/\[\<\>\]/g, \'\');

const safeText = sanitize(\"\<script\>alert(\'XSS\');\</script\>\");

console.log(\"Sanitized:\", safeText);

**6. CSRF (Cross-Site Request Forgery) Prevention**

- Attackers trick users into performing actions on a site without their
  consent.

**Prevention Methods:**

| **Technique**    | **Description**                           |
|------------------|-------------------------------------------|
| CSRF Tokens      | Generate a unique token for each session. |
| SameSite Cookies | Restrict cookies to same-site requests.   |
| Verifying Origin | Check Referer or Origin headers.          |

**Example:**  
In Express.js:

const csrf = require(\"csurf\");

app.use(csrf({ cookie: true }));

app.get(\"/form\", (req, res) =\> {

res.send(\`\<form action=\"/submit\" method=\"POST\"\>

\<input type=\"hidden\" name=\"\_csrf\" value=\"\${req.csrfToken()}\"\>

\<button type=\"submit\"\>Submit\</button\>

\</form\>\`);

});
