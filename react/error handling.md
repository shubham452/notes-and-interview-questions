## ✅ Topics to Know in Error Handling (React)

### 1. **Types of Errors in React Apps**

* **Render-time errors**: When JSX fails to compile or props are incorrect.
* **Async errors**: Failures from promises, `fetch()`, or `setTimeout`.
* **Runtime exceptions**: Example: accessing undefined variables.
* **Network/API errors**: Failed HTTP requests or server errors.
* **Controlled component errors**: Forms not behaving due to state mismatch.

---

### 2. **Error Boundaries (UI-Level Handling)**

```jsx
class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError(error) {
    return { hasError: true };
  }

  componentDidCatch(error, info) {
    console.error("Caught by Error Boundary:", error);
  }

  render() {
    return this.state.hasError ? <h2>Something broke.</h2> : this.props.children;
  }
}

// Usage
<ErrorBoundary>
  <ComponentThatMayFail />
</ErrorBoundary>
```

---

### 3. **Try/Catch Blocks**

Use inside functions that may throw errors:

```jsx
try {
  const data = await fetchData();
} catch (error) {
  console.error("Error fetching:", error);
}
```

---

### 4. **Async/Await Error Handling**

```jsx
const fetchUsers = async () => {
  try {
    const response = await axios.get('/api/users');
    setUsers(response.data);
  } catch (error) {
    setError(error.message);
  }
};
```

---

### 5. **Displaying Fallback/Error UI**

```jsx
{error && <p>Something went wrong: {error}</p>}
```

---

### 6. **Handling API Errors (HTTP codes)**

```jsx
axios.interceptors.response.use(
  res => res,
  err => {
    if (err.response.status === 404) alert("Not found");
    if (err.response.status === 500) alert("Server error");
    return Promise.reject(err);
  }
);
```

---

### 7. **Global Error Logging**

```jsx
componentDidCatch(error, errorInfo) {
  logToService(error, errorInfo); // e.g. Sentry, LogRocket
}
```

---

### 8. **Form Validation Errors**

```jsx
import { useForm } from 'react-hook-form';

const { register, handleSubmit, formState: { errors } } = useForm();

<input {...register("email", { required: true })} />
{errors.email && <span>Email is required</span>}
```

---

### 9. **Network Timeout/Error Handling**

```jsx
axios.get('/api/data', { timeout: 5000 })
  .catch(err => setError("Request timed out"));
```

---

### 10. **UI Error Patterns**

```jsx
{loading && <Skeleton />}
{error && <Toast message="Failed to load" />}
<button onClick={retry}>Retry</button>
```

---

### 11. **Error Handling in Hooks**

```jsx
function useFetch(url) {
  const [data, setData] = useState(null);
  const [error, setError] = useState(null);

  useEffect(() => {
    fetch(url)
      .then(res => res.json())
      .then(setData)
      .catch(setError);
  }, [url]);

  return { data, error };
}
```

---

### 12. **React Query / SWR Error Boundaries**

```jsx
const { data, isError, error } = useQuery('posts', fetchPosts);

if (isError) return <p>Error: {error.message}</p>;
```

---

### 🧠 Key Takeaways

* Not a new mode—just a set of features available automatically in React 18.
* Improves user experience during rendering.
* Does not break existing apps—fully backward compatible.

---

Would you like examples of `useTransition`, `Suspense`, or `useDeferredValue` next?


**✅ Best Practices Summary**

  **Scenario**                **Recommended Handling**
  --------------------------- ------------------------------------------
  Component render crash      Error Boundaries
  Async logic (fetch, etc.)   Try/Catch with Toast feedback
  Lazy loading                Suspense with fallback UI
  App-wide feedback           Toast notifications (error/success/info)



  Here’s a structured breakdown of the **essential topics you need to know for Error Handling in React**, covering both **UI-level** and **code-level** practices — important for interviews, production apps, and debugging.

---

## ✅ Topics to Know in Error Handling (React)

---

### 1. **Types of Errors in React Apps**

* **Render-time errors** (JSX, props issues)
* **Async errors** (fetch, promises, `setTimeout`)
* **Runtime exceptions** (e.g., undefined variables)
* **Network/API errors** (status codes, timeouts)
* **Controlled component errors** (form states)

---

### 2. **Error Boundaries (UI-Level Handling)**

* Catch errors during rendering or lifecycle in a subtree
* Must use class components
* Provide fallback UI + logging
* **Catches:**

  * Rendering
  * Lifecycle
  * Constructors
* **Does not catch:**

  * Event handlers
  * Async callbacks
  * SSR errors

---

### 3. **Try/Catch Blocks**

* Wrap logic that could throw errors
* Best for:

  * API calls
  * Non-React logic
  * Custom utility functions

```jsx
try {
  const data = await fetchData();
} catch (error) {
  console.error(error);
}
```

---

### 4. **Async/Await Error Handling**

* Handle rejected Promises
* Use `try/catch` or `.catch()` on `fetch`, `axios`, etc.

```jsx
const fetchUsers = async () => {
  try {
    const response = await axios.get('/api/users');
  } catch (error) {
    setError(error.message);
  }
};
```

---

### 5. **Displaying Fallback/Error UI**

* Show user-friendly error messages
* Hide broken UI parts
* Provide retry button or support link

```jsx
{error && <p>Something went wrong: {error}</p>}
```

---

### 6. **Handling API Errors (HTTP codes)**

* Show appropriate messages for:

  * 400 (Bad Request)
  * 401 (Unauthorized)
  * 403 (Forbidden)
  * 404 (Not Found)
  * 500 (Server Error)
* Can be handled using axios interceptors or manual logic

---

### 7. **Global Error Logging**

* Use services like:

  * Sentry
  * LogRocket
  * Bugsnag
  * Firebase Crashlytics
* Capture stack trace + user context

---

### 8. **Form Validation Errors**

* Handle input-level errors
* Use libraries like:

  * `react-hook-form`
  * `formik`
  * `yup` for schema validation

---

### 9. **Network Timeout/Error Handling**

* Retry failed requests with delay
* Use retry logic in fetch/axios
* Show offline fallback (e.g., “Please check your internet”)

---

### 10. **UI Error Patterns**

* Show Skeletons, Spinners, or Loaders before error occurs
* Retry mechanism (`Retry` button)
* Toast notifications for errors
* Inline error messages (e.g., under a field)

---

### 11. **Error Handling in Hooks**

* Handle async logic carefully inside `useEffect`
* Don’t throw raw exceptions from custom hooks
* Return error state from custom hooks and render fallback UI

---

### 12. **React Query / SWR Error Boundaries**

* Built-in support for error handling in hooks
* Use `isError` and `error` returned by hooks

```jsx
const { data, isError, error } = useQuery('posts', fetchPosts);

if (isError) return <p>Error: {error.message}</p>;
```

---

Would you like me to:

* Add these notes to your doc?
* Turn this into an interview-ready Q\&A format?
* Provide examples with axios, React Query, and Error Boundaries?

