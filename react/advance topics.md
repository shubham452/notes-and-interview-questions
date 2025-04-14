**⚛️ 1. What is Concurrent Mode in React?**

**Concurrent Mode** is a set of features in React that helps make
rendering **non-blocking** and **interruptible**. It improves
performance and user experience by allowing React to:

-   Interrupt rendering to handle more urgent updates

-   Render components **in the background**

-   Keep the UI **responsive and fluid**

🔸 It enables features like Suspense, useTransition, and **better
prioritization of updates**.

**⏳ 2. How does Suspense work in React?**

**Suspense** lets you wait for **some async resource** (like
code-splitting or data fetching) and **show a fallback UI** while
waiting.

jsx

import React, { Suspense, lazy } from \'react\';

const LazyComponent = lazy(() =\> import(\'./LazyComponent\'));

function App() {

return (

\<Suspense fallback={\<div\>Loading\...\</div\>}\>

\<LazyComponent /\>

\</Suspense\>

);

}

🔹 Suspense can now also be used with data fetching (with React 18 and
libraries like React Query or Relay).

**🧠 3. What is the difference between hydration and rendering?**

  ------------------------------------------------------------------------------
  **Term**        **Explanation**
  --------------- --------------------------------------------------------------
  **Rendering**   Generating and inserting the HTML into the DOM (client or
                  server).

  **Hydration**   The process where React attaches event handlers and makes a
                  static HTML page **interactive**.
  ------------------------------------------------------------------------------

🔹 Hydration is used in **Server-Side Rendering (SSR)** to convert
static markup into a live React app.

**🔌 4. What are React Portals, and when should you use them?**

**React Portals** let you render children into a **different DOM
subtree**, outside the parent component hierarchy.

jsx

ReactDOM.createPortal(child, container);

📦 Example use case:

jsx

createPortal(\<Modal /\>, document.getElementById(\'modal-root\'));

✅ **Use Portals for:**

-   Modals

-   Tooltips

-   Dropdowns

-   Toasts

🔸 They solve z-index and overflow issues by escaping parent stacking
contexts.

**🛡️ 5. What is the purpose of Error Boundaries in React?**

**Error Boundaries** catch JavaScript errors **in child components**
during rendering, lifecycle methods, and constructors, and show a
fallback UI.

jsx

class ErrorBoundary extends React.Component {

state = { hasError: false };

static getDerivedStateFromError() {

return { hasError: true };

}

componentDidCatch(error, info) {

console.error(\"Caught by boundary:\", error, info);

}

render() {

if (this.state.hasError) return \<h1\>Something went wrong.\</h1\>;

return this.props.children;

}

}

🔹 They **don't catch** errors in event handlers, async code, or
server-side rendering.

**🐢 6. How does React handle lazy loading?**

React uses **React.lazy()** and **Suspense** to **code-split**
components and load them only when needed (i.e., on-demand).

jsx

const LazyComp = React.lazy(() =\> import(\'./HeavyComponent\'));

\<Suspense fallback={\<Loading /\>}\>

\<LazyComp /\>

\</Suspense\>

✅ Benefits:

-   Reduces initial bundle size

-   Improves page load speed

🔹 Works well with routing and dynamic import strategies.
