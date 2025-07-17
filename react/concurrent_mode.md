✅ React Concurrent Mode (a.k.a. Concurrent Features in React 18+)

🔍 What is Concurrent Mode?

Concurrent Mode is a set of features that enable React to prepare multiple versions of the UI at the same time. It improves responsiveness by allowing React to interrupt, pause, resume, or abandon rendering.

✅ Why is it Useful?

Traditional React rendering is synchronous and blocking. If a component takes time to render, it may delay updates to the screen. Concurrent Mode solves this by making rendering non-blocking.

Benefits:

Makes apps more responsive.

Allows React to pause and resume rendering work.

Enables prioritization of urgent vs non-urgent updates.

🔧 How to Enable Concurrent Features

React 18 enables concurrent features automatically when using createRoot() instead of ReactDOM.render().

import { createRoot } from 'react-dom/client';

const root = createRoot(document.getElementById('root'));
root.render(<App />);

🛠️ Key Features

1. startTransition()

Marks updates as non-urgent so React can interrupt them if needed.

startTransition(() => {
  setState(newState);
});

2. useTransition()

Provides loading state while deferring updates.

const [isPending, startTransition] = useTransition();

startTransition(() => {
  setQuery(value);
});

3. useDeferredValue()

Defer low-priority updates until high-priority updates are complete.

const deferredQuery = useDeferredValue(query);

4. Suspense

Used to show fallback UI while a component is lazily loading or waiting for data.

<Suspense fallback={<Loading />}>
  <MyComponent />
</Suspense>

📚 Topics to Know in Concurrent Mode (React 18+)

1. What is Concurrent Mode?

Concurrent Mode allows React to work on multiple tasks simultaneously by interrupting and prioritizing rendering work. This helps avoid blocking the UI and improves responsiveness during complex updates.

2. How to Enable Concurrent Features

With React 18, Concurrent Features are enabled automatically when you use createRoot() instead of ReactDOM.render(). This requires no configuration or mode flags.

3. Core APIs & Hooks

startTransition(): Wraps updates that can be deferred (like filtering large lists). Prevents UI blocking during slow updates.

useTransition(): Lets you mark certain UI updates as low-priority and gives you a boolean isPending to show loading indicators.

useDeferredValue(): Defers updates of a value to avoid lag when UI responds to fast input like typing.

Suspense: Shows fallback UI while waiting for async components or data (e.g., lazy loading).

4. Automatic Batching

React batches multiple state updates together — even inside setTimeout, promises, or async functions — to reduce re-renders and improve performance.

5. Interruptible Rendering

React can pause rendering large or low-priority trees and resume them later. This keeps the app responsive, especially on slow devices.

6. Selective Hydration (for SSR)

In server-side rendered apps, React prioritizes the hydration of visible elements first, improving Time-To-Interactive.

7. Concurrent Rendering vs Concurrent Execution

Concurrent Rendering is React’s internal scheduling model. JavaScript itself remains single-threaded — React just splits work into chunks and defers low-priority tasks smartly.

💻 Code Examples for Concurrent Features

✅ useTransition() Example:

import { useState, useTransition } from 'react';

function SearchComponent() {
  const [input, setInput] = useState('');
  const [list, setList] = useState([]);
  const [isPending, startTransition] = useTransition();

  const handleChange = (e) => {
    const value = e.target.value;
    setInput(value);

    startTransition(() => {
      const filtered = filterHeavyData(value); // assume this is a costly operation
      setList(filtered);
    });
  };

  return (
    <>
      <input value={input} onChange={handleChange} />
      {isPending && <p>Loading...</p>}
      <List items={list} />
    </>
  );
}

✅ useDeferredValue() Example:

import { useDeferredValue } from 'react';

function SearchResults({ query }) {
  const deferredQuery = useDeferredValue(query);
  const results = searchInBigList(deferredQuery);

  return (
    <ul>
      {results.map(item => <li key={item.id}>{item.name}</li>)}
    </ul>
  );
}

✅ Suspense with Lazy-loaded Component:

import React, { Suspense, lazy } from 'react';

const UserProfile = lazy(() => import('./UserProfile'));

function App() {
  return (
    <Suspense fallback={<p>Loading user profile...</p>}>
      <UserProfile />
    </Suspense>
  );
}

🧠 Key Takeaways

Not a new mode—just a set of features available automatically in React 18.

Improves user experience during rendering.

Does not break existing apps—fully backward compatible.
