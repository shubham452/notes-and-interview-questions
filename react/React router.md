**🚦 React Router**

**1. What is React Router?**

React Router is a standard routing library for React that enables
navigation among views of different components, allowing single-page
applications (SPA) to simulate multi-page behavior.

It provides dynamic routing by using component structure and manages the
URL state in sync with the UI.

**2. What is the difference between BrowserRouter and HashRouter?**

 | Feature         | Clean URLs (`/about`)           | Hash-based URLs (`#/about`)        |
|----------------|----------------------------------|------------------------------------|
| URL Format     | Uses clean URLs (`/about`)       | Uses hash-based URLs (`#/about`)   |
| Server Support | Requires server-side support for routes | No server support needed       |
| History API    | Uses HTML5 History API           | Uses hash portion of the URL       |


**3. How do you handle route parameters in React Router?**

jsx

&lt;Route path="/user/:id" element={&lt;User /&gt;} /&gt;

You can access the parameter using the useParams hook:

jsx

import { useParams } from 'react-router-dom';

const User = () =&gt; {

const { id } = useParams();

return &lt;div&gt;User ID: {id}&lt;/div&gt;;

};

**4. What is lazy loading in React Router?**

Lazy loading delays the loading of components until they are needed,
improving performance.

jsx

import { lazy, Suspense } from 'react';

const Home = lazy(() =&gt; import('./Home'));

&lt;Suspense fallback={&lt;div&gt;Loading...&lt;/div&gt;}&gt;

&lt;Route path="/" element={&lt;Home /&gt;} /&gt;

&lt;/Suspense&gt;

**5. How do you create a private route in React Router?**

Private routes restrict access based on authentication.

jsx

const PrivateRoute = ({ children }) =&gt; {

const isAuthenticated = /\* your auth logic \*/;

return isAuthenticated ? children : &lt;Navigate to="/login" /&gt;;

};

// Usage

&lt;Route path="/dashboard" element={&lt;PrivateRoute&gt;&lt;Dashboard
/&gt;&lt;/PrivateRoute&gt;} /&gt;

**6. What is the difference between useNavigate and useHistory?**

 | **Hook**       | **React Router Version** | **Description**                            |
|----------------|---------------------------|--------------------------------------------|
| `useHistory`   | v5                        | Used to access navigation history          |
| `useNavigate`  | v6+                       | Replaces `useHistory`, more declarative    |


Example:


const navigate = useNavigate();

navigate('/home');

🌐 1. react-router-dom Basics
----------------------------

### ✅ Core Components

| **Component**    | **Purpose**                                                             |
|------------------|--------------------------------------------------------------------------|
| `BrowserRouter`  | Wraps the app to enable routing using the HTML5 history API             |
| `Routes`         | Replaces `Switch` (v6+). Holds all the route definitions                |
| `Route`          | Defines a single route path and the element to render                   |


### 🔰 Example:

jsx

import { BrowserRouter, Routes, Route } from 'react-router-dom';

import Home from './Home';

import About from './About';

function App() {

return (

&lt;BrowserRouter&gt;

&lt;Routes&gt;

&lt;Route path="/" element={&lt;Home /&gt;} /&gt;

&lt;Route path="/about" element={&lt;About /&gt;} /&gt;

&lt;/Routes&gt;

&lt;/BrowserRouter&gt;

);

}

🧩 2. Nested Routes
------------------

-   Useful when a route should render sub-routes inside a parent layout.

-   Use &lt;Outlet /&gt; in the parent component to render child routes.

### 📦 Example:

jsx

// In App.js

&lt;Routes&gt;

&lt;Route path="/dashboard" element={&lt;Dashboard /&gt;}&gt;

&lt;Route path="profile" element={&lt;Profile /&gt;} /&gt;

&lt;Route path="settings" element={&lt;Settings /&gt;} /&gt;

&lt;/Route&gt;

&lt;/Routes&gt;

jsx

// In Dashboard.js

import { Outlet } from 'react-router-dom';

const Dashboard = () =&gt; (

&lt;div&gt;

&lt;h1&gt;Dashboard&lt;/h1&gt;

&lt;Outlet /&gt; {/\* Nested routes will render here \*/}

&lt;/div&gt;

);

🚀 3. Navigation (useNavigate, Link)
-----------------------------------

### 🔗 Link

-   Used to render anchor-style navigation without reloading the page.

jsx

&lt;Link to="/about"&gt;About&lt;/Link&gt;

### 📍 useNavigate

-   Programmatic navigation (like history.push() in older versions).

jsx

import { useNavigate } from 'react-router-dom';

const Home = () =&gt; {

const navigate = useNavigate();

const goToProfile = () =&gt; navigate('/profile');

return &lt;button onClick={goToProfile}&gt;Go to Profile&lt;/button&gt;;

};
**Link** is a React component from react-router-dom that's used to create navigation links in your JSX. It’s like an anchor tag (), but it prevents a full page reload and lets React Router handle the route change smoothly.


You use this when you want users to click and go to another page.

**useNavigate** is a hook also from react-router-dom. You use it inside a function (like after submitting a form) to programmatically navigate to another route.

Example:

useNavigate();  const handleSubmit = () => {    // after some logic    navigate('/dashboard');  };   `

So basically:

*   Use Link when you're navigating through the UI (clickable links).
    
*   Use useNavigate when you need to redirect in code after some action or logic.

🔢 4. URL Params (useParams)
---------------------------

-   Useful for dynamic routes like /users/:id

### 🧪 Example:

jsx

// Route definition

&lt;Route path="/users/:id" element={&lt;User /&gt;} /&gt;

// User.js

import { useParams } from 'react-router-dom';

const User = () =&gt; {

const { id } = useParams();

return &lt;div&gt;User ID: {id}&lt;/div&gt;;

};

🔁 5. Redirects and Route Protection
-----------------------------------

### 🔄 Redirect using useNavigate

jsx

const navigate = useNavigate();

useEffect(() =&gt; {

if (!userLoggedIn) {

navigate('/login');

}

}, \[\]);

### 🔐 Route Protection (Private Routes)

You can create a wrapper component to protect routes.

#### 🔒 PrivateRoute Component

jsx

const PrivateRoute = ({ children }) =&gt; {

const isAuthenticated = localStorage.getItem('token');

return isAuthenticated ? children : &lt;Navigate to="/login" /&gt;;

};

#### ✅ Usage:

jsx

&lt;Routes&gt;

&lt;Route path="/login" element={&lt;Login /&gt;} /&gt;

&lt;Route path="/dashboard" element={&lt;PrivateRoute&gt;&lt;Dashboard
/&gt;&lt;/PrivateRoute&gt;} /&gt;

&lt;/Routes&gt;
