1. Router Setup
BrowserRouter vs HashRouter

Wrapping your app with <BrowserRouter>

Static vs dynamic routes

2. Routes & Route
<Routes> and <Route> usage (v6+)

Nested <Route> configuration

Route path matching (exact match no longer needed in v6)

Using index routes for default child components

3. Navigation Components
<Link> vs <NavLink> (with styling)

<Navigate /> for programmatic redirection

<Outlet /> for nested routing rendering

4. Route Parameters
useParams() hook

Dynamic segments like /user/:id

Optional parameters and splat routes (*)

5. Programmatic Navigation
useNavigate() hook to navigate manually (replace vs push)

Passing state via navigation

6. Hooks
useLocation() (access current URL info)

useParams() (access route parameters)

useNavigate() (programmatic routing)

7. Nested Routes
Route nesting via parent <Route> and <Outlet />

Handling nested layouts and child components

Using layout routes for common wrappers (e.g., sidebar)

8. Conditional Rendering / Access Control
Redirecting unauthenticated users

PrivateRoute / Protected Route pattern (custom wrapper)

Role-based routing guards

9. 404 Not Found Handling
Wildcard * route

Fallback route with custom 404 page

10. Code Splitting with Lazy Routes
React.lazy and Suspense with routes

Loading components lazily to optimize performance

11. Query Parameters (optional)
Using useLocation() + URLSearchParams to read query strings

Handling filters/sorting/search via query params

12. Outlet Context (Advanced)
Passing data to nested routes using <Outlet context={...} />

Reading with useOutletContext()

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


**🧭 React Router Notes (v6+) with Examples**

---

## 1. **Router Setup**

### `BrowserRouter` vs `HashRouter`

* `BrowserRouter`: Uses HTML5 history API (clean URLs like `/home`).
* `HashRouter`: Uses hash in URL (`/#/home`). Useful when deploying on static hosts without backend support.

**Example:**

```jsx
import { BrowserRouter } from 'react-router-dom';

<BrowserRouter>
  <App />
</BrowserRouter>
```

---

## 2. **Routes & Route**

* Wrap all routes inside `<Routes>`.
* Use `<Route path="..." element={<Component />} />`.

**Example:**

```jsx
<Routes>
  <Route path="/" element={<Home />} />
  <Route path="/about" element={<About />} />
</Routes>
```

---

## 3. **Navigation Components**

### `Link` vs `NavLink`

* `Link`: Basic navigation.
* `NavLink`: Adds `active` styling when route matches.

**Example:**

```jsx
<Link to="/about">About</Link>
<NavLink to="/home" className={({ isActive }) => isActive ? 'active' : ''}>Home</NavLink>
```

---

## 4. **Route Parameters**

Use `:id` in the path and `useParams()` to read it.

**Example:**

```jsx
<Route path="/user/:id" element={<UserProfile />} />
```

```jsx
function UserProfile() {
  const { id } = useParams();
  return <div>User ID: {id}</div>;
}
```

---

## 5. **Programmatic Navigation**

Use `useNavigate()` to redirect manually.

**Example:**

```jsx
const navigate = useNavigate();
navigate('/dashboard');
navigate('/login', { replace: true });
```

---

## 6. **React Router Hooks**

* `useParams()` – Get URL params.
* `useLocation()` – Get current URL info.
* `useNavigate()` – Navigate programmatically.

---

## 7. **Nested Routes & Layouts**

Use `<Outlet />` in layout components to render nested children.

**Example:**

```jsx
<Route path="/dashboard" element={<DashboardLayout />}>
  <Route index element={<DashboardHome />} />
  <Route path="settings" element={<Settings />} />
</Route>
```

```jsx
function DashboardLayout() {
  return (
    <>
      <Sidebar />
      <Outlet />
    </>
  );
}
```

---

## 8. **Protected Routes (Auth)**

Wrap protected routes in a component that checks auth.

**Example:**

```jsx
function PrivateRoute({ children }) {
  const isLoggedIn = !!localStorage.getItem('token');
  return isLoggedIn ? children : <Navigate to="/login" />;
}

<Route path="/admin" element={<PrivateRoute><Admin /></PrivateRoute>} />
```

---

## 9. **404 - Page Not Found**

Catch all unmatched routes using `*`.

**Example:**

```jsx
<Route path="*" element={<NotFound />} />
```

---

## 10. **Lazy Loading Routes**

Use `React.lazy` + `Suspense` to load routes only when needed.

**Example:**

```jsx
const About = React.lazy(() => import('./About'));

<Route path="/about" element={
  <Suspense fallback={<div>Loading...</div>}>
    <About />
  </Suspense>
} />
```

---

## 11. **Query Parameters**

Use `useLocation()` with `URLSearchParams`.

**Example:**

```jsx
const { search } = useLocation();
const query = new URLSearchParams(search);
const name = query.get('name');
```

---

## 12. **Outlet Context**

Use `<Outlet context={value}>` to pass data to nested routes.

**Example:**

```jsx
<Outlet context={{ user }} />
```

```jsx
const { user } = useOutletContext();
```

---

| Feature                    | `useParams()`                            | `useQuery` (via `useLocation`)                                  |
| -------------------------- | ---------------------------------------- | --------------------------------------------------------------- |
| **Purpose**                | Get route/path parameters (URL segments) | Get **query parameters** (key=value in URL)                     |
| **Source of Data**         | Comes from the path itself (`/user/:id`) | Comes from the query string (`?page=2&sort=asc`)                |
| **React Router Built-in?** | ✅ Yes (`react-router-dom`)               | ❌ No direct `useQuery`, use `useLocation()` + `URLSearchParams` |
| **Example URL**            | `/user/42`                               | `/user?page=2&sort=asc`                                         |

## ✅ `useParams()` – For Path Parameters

### Example:
```jsx
<Route path="/user/:id" element={<User />} />


import { useParams } from 'react-router-dom';

import { useParams } from 'react-router-dom';

function User() {
  const { id } = useParams(); // '42' if URL is /user/42
  return <p>User ID: {id}</p>;
}

✅ useQuery (Custom Hook using useLocation) – For Query Strings
Example:
URL: /products?page=2&sort=price


import { useLocation } from 'react-router-dom';

function useQuery() {
  return new URLSearchParams(useLocation().search);
}

function ProductList() {
  const query = useQuery();
  const page = query.get("page");  // '2'
  const sort = query.get("sort");  // 'price'

  return <p>Page: {page}, Sort by: {sort}</p>;
}

| Scenario                    | Use                                              |
| --------------------------- | ------------------------------------------------ |
| `/product/123`              | `useParams()`                                    |
| `/product?id=123&filter=on` | `useLocation()` + `URLSearchParams` (`useQuery`) |

