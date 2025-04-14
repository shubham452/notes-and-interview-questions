**✅ What are React Hooks?**

**Hooks** are functions that let you **use state and lifecycle
features** in functional components.\
They enable functional components to have side effects, manage context,
refs, memoization, etc.

**✅ What are the rules of hooks?**

1.  ✅ **Only call hooks at the top level** (not inside loops,
    conditions, or nested functions).

2.  ✅ **Only call hooks from React functions** (components or
    custom hooks).

**✅ What is useState, and how does it work?**

useState lets you **add state** to functional components.

jsx

const \[count, setCount\] = useState(0);

-   count is the current state.

-   setCount updates it and triggers a re-render.

**✅ How does useEffect work, and what are its use cases?**

useEffect lets you run **side effects** (e.g., fetch calls, DOM
manipulation).

jsx

useEffect(() =&gt; {

console.log("Component mounted or updated");

}, \[dependency\]);

**Use cases:**

-   Fetching data

-   Setting up subscriptions

-   Cleanup (return a function)

**✅ What is useContext, and when should you use it?**

useContext allows access to **context values** in functional components
without prop drilling.

jsx

const theme = useContext(ThemeContext);

Use it when multiple components need **shared global data** like theme,
auth, or locale.

**✅ Explain useReducer and its benefits over useState.**

useReducer is a hook for **complex state logic**, similar to Redux-style
reducers.

jsx

const \[state, dispatch\] = useReducer(reducer, initialState);

**Benefits over useState:**

-   Better for **multiple related state updates**

-   Keeps logic centralized

-   Easier debugging and testability

**✅ How do useRef and forwardRef work in React?**

-   **useRef** creates a **mutable reference** that persists
    across renders.

jsx

const inputRef = useRef(null);

&lt;input ref={inputRef} /&gt;

-   **forwardRef** passes a ref from a parent to a child component.

jsx

const FancyInput = forwardRef((props, ref) =&gt; (

&lt;input ref={ref} {...props} /&gt;

));

**✅ What is useMemo, and when should it be used?**

useMemo **memoizes the result** of a function to avoid expensive
recalculations.

jsx

const result = useMemo(() =&gt; computeExpensiveValue(a, b), \[a, b\]);

Use it to **optimize performance** in:

-   Expensive computations

-   Avoiding re-renders of pure components

**✅ How does useCallback optimize performance?**

useCallback memoizes a **function definition**, so it’s not recreated on
every render.

jsx

const handleClick = useCallback(() =&gt; {

doSomething();

}, \[dependency\]);

Use it to:

-   Prevent unnecessary re-renders

-   Optimize components using React.memo or props with functions

**✅ How can you create a custom hook in React?**

A custom hook is just a **reusable function** that uses other hooks.

jsx

function useCounter(initial = 0) {

const \[count, setCount\] = useState(initial);

const increment = () =&gt; setCount((c) =&gt; c + 1);

return { count, increment };

}

Use custom hooks to extract and reuse logic cleanly.

✅ **1.** useState**,** useEffect
--------------------------------

  **Hook**    **Purpose**                                    **Example**
  ----------- ---------------------------------------------- -----------------------------------------
  useState    Local state management                         const \[count, setCount\] = useState(0)
  useEffect   Side effects (fetching, subscriptions, etc.)   useEffect(() =&gt; { ... }, \[deps\])

🧩 **2.** useContext**,** useReducer
-----------------------------------

  **Hook**     **Purpose**                        **Use Case**
  ------------ ---------------------------------- ------------------------------------
  useContext   Access values from React Context   Theme, Auth, User info
  useReducer   Complex state logic with actions   Form management, counters, toggles

🧠 **3.** useRef**,** useMemo**,** useCallback
---------------------------------------------

  **Hook**      **Purpose**                          **Example Use Case**
  ------------- ------------------------------------ ------------------------------------
  useRef        Persistent mutable value, DOM refs   Access input element, store timers
  useMemo       Memoize expensive computation        Heavy calculations
  useCallback   Memoize function instance            Prevent unnecessary child renders

jsx

const inputRef = useRef(null);

const memoizedValue = useMemo(() =&gt; compute(value), \[value\]);

const memoizedFn = useCallback(() =&gt; doSomething(), \[\]);

⚙️ **4.** useLayoutEffect**,** useImperativeHandle
--------------------------------------------------

  **Hook**              **Purpose**                                  **Example Use Case**
  --------------------- -------------------------------------------- ------------------------------
  useLayoutEffect       Like useEffect but fires **before** paint    Measure DOM, sync layout
  useImperativeHandle   Customize value exposed by ref from parent   Call child functions via ref

jsx

useLayoutEffect(() =&gt; {

// Read/measure DOM

}, \[\]);

useImperativeHandle(ref, () =&gt; ({

focus: () =&gt; inputRef.current.focus()

}));

⏳ **5.** useId**,** useTransition**,** useDeferredValue
-------------------------------------------------------

  **Hook**           **Purpose**                              **Example Use Case**
  ------------------ ---------------------------------------- ----------------------------------------
  useId              Generate unique IDs (SSR-safe)           Form labels & inputs
  useTransition      Mark updates as **non-urgent**           Low-priority updates (e.g., filtering)
  useDeferredValue   Defer re-render of slow-changing value   Smooth UI while typing/searching

jsx

const id = useId();

const \[isPending, startTransition\] = useTransition();

startTransition(() =&gt; {

setValue(newValue);

});

const deferredQuery = useDeferredValue(query);
