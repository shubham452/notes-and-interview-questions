**⚡ Performance Optimization in React**

**1. What are common performance issues in React?**

-   Unnecessary re-renders

-   Large component trees

-   Inefficient state management

-   Non-memoized functions/values causing re-renders

-   Large list rendering without virtualization

-   Blocking the main thread with heavy computations

**2. How do you optimize React rendering performance?**

-   Use React.memo to prevent unnecessary re-renders

-   Split large components into smaller ones

-   Use useCallback and useMemo

-   Avoid updating state unnecessarily

-   Lazy load components (code splitting)

-   Virtualize long lists using react-window or react-virtualized

-   Debounce or throttle expensive functions

-   Use the key prop effectively in lists

**3. What is React.memo, and when should it be used?**

React.memo is a **higher-order component** that memoizes the result of a
component and prevents re-renders unless props change.

js

const MyComponent = React.memo((props) =&gt; {

return &lt;div&gt;{props.value}&lt;/div&gt;;

});

**Use it when:**

-   The component renders the same output for the same props

-   It’s a pure functional component

-   Performance is a concern due to frequent re-renders

**4. How does useMemo help in optimization?**

useMemo **memoizes the return value** of a computation, recomputing it
only when dependencies change.

js

const expensiveValue = useMemo(() =&gt; computeExpensive(val), \[val\]);

**Use when:**

-   The computation is expensive

-   Avoiding recalculation on every render matters

**5. What is the difference between useCallback and useMemo?**

  **Hook**      **Purpose**                    **Returns**
  ------------- ------------------------------ -----------------
  useMemo       Memoizes computed **values**   Cached value
  useCallback   Memoizes **functions**         Cached function

js

const memoizedCallback = useCallback(() =&gt; doSomething(a, b), \[a,
b\]);

**6. How can you optimize large lists in React?**

-   Use **windowing/virtualization** with libraries like:

    -   react-window

    -   react-virtualized

-   Render only the visible portion of the list

-   Use key props correctly

-   Avoid heavy rendering logic inside list items

**7. What is the significance of the shouldComponentUpdate lifecycle
method?**

Used in **class components** to **prevent unnecessary re-renders** by
comparing current and next props/state.

js

shouldComponentUpdate(nextProps, nextState) {

return nextProps.value !== this.props.value;

}

**8. What are Pure Components in React?**

A **PureComponent** is a class component that implements
shouldComponentUpdate with a **shallow prop/state comparison**.

js

class MyComponent extends React.PureComponent {

render() {

return &lt;div&gt;{this.props.name}&lt;/div&gt;;

}

}

**9. What is code splitting, and how does React support it?**

Code splitting allows you to **split your code into chunks** and load
them on demand.

React supports it using:

-   React.lazy() for dynamic imports

-   Suspense for fallback UI

js

const LazyComponent = React.lazy(() =&gt; import('./LazyComponent'));

&lt;Suspense fallback={&lt;div&gt;Loading...&lt;/div&gt;}&gt;

&lt;LazyComponent /&gt;

&lt;/Suspense&gt;

**10. How does React handle reconciliation?**

**Reconciliation** is the process by which React **updates the DOM** by
comparing the current and previous virtual DOM trees.

Steps:

-   Compares elements by **type**

-   Uses **keys** to track changes in lists

-   Tries to reuse existing DOM nodes when possible

-   Minimizes actual DOM mutations for performance

**⚡ 1. Memoization Techniques**

**✅ React.memo**

-   Wraps a **component** to prevent re-renders if props
    haven’t changed.

jsx

const MyComponent = React.memo(({ name }) =&gt; {

console.log("Rendered");

return &lt;div&gt;{name}&lt;/div&gt;;

});

**✅ useMemo**

-   Memoizes a **computed value** to avoid recalculating on
    every render.

jsx

const expensiveValue = useMemo(() =&gt; computeHeavy(a, b), \[a, b\]);

**✅ useCallback**

-   Memoizes a **function reference** to prevent child components from
    re-rendering due to function recreation.

jsx

const handleClick = useCallback(() =&gt; {

doSomething();

}, \[dependency\]);

**🐢 2. Lazy Loading Components**

**✅ React.lazy + Suspense**

-   Dynamically loads components to reduce initial bundle size.

jsx

const LazyAbout = React.lazy(() =&gt; import('./About'));

&lt;Suspense fallback={&lt;div&gt;Loading...&lt;/div&gt;}&gt;

&lt;LazyAbout /&gt;

&lt;/Suspense&gt;

**📦 3. Code Splitting**

-   Automatically happens with dynamic import() in React.lazy.

-   Can also use tools like Webpack + route-based code splitting with
    React Router.

jsx

&lt;Route path="/about" element={

&lt;Suspense fallback={&lt;Loading /&gt;}&gt;

&lt;LazyAbout /&gt;

&lt;/Suspense&gt;

} /&gt;

**🔁 4. Avoiding Unnecessary Re-renders**

-   Use React.memo, useMemo, useCallback.

-   Keep state close to where it's used.

-   Avoid anonymous functions/objects in props.

-   Use stable keys in lists.

-   Don’t mutate state directly.

**📋 5. List Rendering with Keys**

-   Keys help React identify which items changed.

-   Use **stable unique keys** (not index if list order may change).

jsx

{users.map(user =&gt; &lt;User key={user.id} {...user} /&gt;)}

**🪟 6. Virtualization**

-   Renders only visible items in large lists to improve performance.

**✅ Libraries:**

-   react-window

-   react-virtualized

**✨ Example (react-window):**

jsx

import { FixedSizeList as List } from 'react-window';

&lt;List

height={400}

itemCount={1000}

itemSize={35}

width={300}

&gt;

{({ index, style }) =&gt; &lt;div style={style}&gt;Item
{index}&lt;/div&gt;}

&lt;/List&gt;
