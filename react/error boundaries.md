Here are the **must-know topics for Error Boundaries in React**, especially for interviews and real-world debugging scenarios:

---

## ✅ Topics to Know in Error Boundaries (React)

### 1. **What Are Error Boundaries?**

* Special React components that **catch JavaScript errors** in the component tree **during rendering**, in lifecycle methods, and in constructors.
* Prevent the entire app from crashing by **gracefully handling exceptions** and showing fallback UI.

---

### 2. **How to Create an Error Boundary**

* Must be a **class component**
* Must implement at least one of:

  * `static getDerivedStateFromError()`
  * `componentDidCatch()`

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
    console.error("Error caught:", error, info);
  }

  render() {
    if (this.state.hasError) {
      return <h2>Something went wrong.</h2>;
    }

    return this.props.children;
  }
}
```

---

### 3. **Where to Place Error Boundaries**

* Around parts of the UI that are most likely to fail (e.g. third-party widgets, large components, feature modules).
* Wrap at different levels to isolate specific parts of the UI instead of the whole app.

```jsx
<ErrorBoundary>
  <Profile />
</ErrorBoundary>
```

---

### 4. **What Error Boundaries Can Catch**

✅ Catches:

* Rendering errors in child components
* Errors in lifecycle methods
* Errors in constructors of the child tree

❌ Does NOT catch:

* Errors in **event handlers**
* Errors in **async code** (e.g. `setTimeout`)
* Server-side rendering errors
* Errors outside React (e.g., global variables)

---

### 5. **Fallback UI**

* Can be a message, image, retry button, or custom layout.
* React 18 also allows **lazy fallback rendering** with `Suspense` for lazy-loaded components.

---

### 6. **Logging & Monitoring**

* Use `componentDidCatch(error, info)` to send error data to a logging service (e.g., Sentry, LogRocket).

---

### 7. **Why Not Functional Components?**

* Currently, error boundaries **must be class components** because `componentDidCatch` is a class lifecycle method.
* React may support this in the future via hooks (e.g., `useErrorBoundary`) — not yet officially.

---

### 8. **Combining with Suspense**

* `Suspense` handles async/lazy loading.
* `ErrorBoundary` handles runtime JS errors.
* Use both for robust UI recovery.

```jsx
<ErrorBoundary>
  <Suspense fallback={<Spinner />}>
    <LazyComponent />
  </Suspense>
</ErrorBoundary>
```

---

Would you like me to:

* Add this into your doc?
* Create a summary table or PDF for Error Boundaries?
* Generate interview questions based on this?
