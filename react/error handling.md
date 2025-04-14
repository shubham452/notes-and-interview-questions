**🧱 1. Error Boundaries (Class Components Only)**

Used to catch **render-time errors** in child components and display a
fallback UI.

**✅ Key Lifecycle Methods:**

  **Method**                 **Purpose**
  -------------------------- ---------------------------------------
  getDerivedStateFromError   Updates state to show fallback UI
  componentDidCatch          Logs error info (e.g., to monitoring)

**✨ Example:**

jsx

class ErrorBoundary extends React.Component {

state = { hasError: false };

static getDerivedStateFromError(error) {

return { hasError: true };

}

componentDidCatch(error, info) {

console.error("Caught error:", error, info);

}

render() {

if (this.state.hasError) {

return &lt;h2&gt;Something went wrong.&lt;/h2&gt;;

}

return this.props.children;

}

}

**✅ Usage:**

jsx

&lt;ErrorBoundary&gt;

&lt;MyComponent /&gt;

&lt;/ErrorBoundary&gt;

**🔁 2. Try/Catch in Async Functions**

Use try/catch blocks to handle async logic safely, especially in data
fetching.

jsx

const fetchData = async () =&gt; {

try {

const res = await fetch("/api/data");

const data = await res.json();

setData(data);

} catch (err) {

console.error("Fetch error:", err);

toast.error("Failed to fetch data.");

}

};

**🌀 3. Suspense for Loading and Errors**

-   Suspense shows fallback UI while components load (e.g., React.lazy).

-   Error handling must still be done with Error Boundaries for
    thrown errors.

jsx

const LazyComponent = React.lazy(() =&gt; import('./MyComponent'));

&lt;Suspense fallback={&lt;LoadingSpinner /&gt;}&gt;

&lt;LazyComponent /&gt;

&lt;/Suspense&gt;

For error + suspense handling, wrap lazy components with **both**
Suspense and an ErrorBoundary.

**🔔 4. Toast Notifications for UX Feedback**

Use libraries like **react-toastify** or **sonner** for user-friendly
error messages.

**✨ Example with react-toastify:**

bash

npm install react-toastify

jsx

import { toast, ToastContainer } from 'react-toastify';

import 'react-toastify/dist/ReactToastify.css';

toast.error("Something went wrong!");

&lt;ToastContainer position="top-right" autoClose={3000} /&gt;

**✅ Best Practices Summary**

  **Scenario**                **Recommended Handling**
  --------------------------- ------------------------------------------
  Component render crash      Error Boundaries
  Async logic (fetch, etc.)   Try/Catch with Toast feedback
  Lazy loading                Suspense with fallback UI
  App-wide feedback           Toast notifications (error/success/info)
