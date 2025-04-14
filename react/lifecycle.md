**🔄 React Lifecycle Methods**

**1. What are the different lifecycle methods in class components?**

React class components go through **three main lifecycle phases**:

**➤ Mounting (component is being created and inserted into the DOM)**

-   constructor()

-   static getDerivedStateFromProps()

-   render()

-   componentDidMount()

**➤ Updating (re-rendering due to props or state changes)**

-   static getDerivedStateFromProps()

-   shouldComponentUpdate()

-   render()

-   getSnapshotBeforeUpdate()

-   componentDidUpdate()

**➤ Unmounting (component is being removed from the DOM)**

-   componentWillUnmount()

**2. What is the difference between componentDidMount and useEffect?**

  **Feature**   **componentDidMount (Class)**     **useEffect (Function)**
  ------------- --------------------------------- --------------------------------------------------------
  Usage         Only once after mount             Can simulate componentDidMount, DidUpdate, WillUnmount
  Syntax        componentDidMount()               useEffect(() =&gt; { ... }, \[\])
  Purpose       Fetch data, add event listeners   Same, but used in functional components

**3. What is componentDidUpdate, and when is it triggered?**

-   Runs **after every update** (state or props changes).

-   Good for:

    -   **Fetching new data** when props/state changes.

    -   **Interacting with DOM** based on updated values.

js

componentDidUpdate(prevProps, prevState) {

if (this.props.id !== prevProps.id) {

// fetch new data

}

}

**4. What is componentWillUnmount, and why is it useful?**

-   Called **just before the component is removed** from the DOM.

-   Useful for:

    -   **Cleaning up** subscriptions, timers, event listeners, etc.

js

componentWillUnmount() {

clearInterval(this.timer);

}

**5. How does shouldComponentUpdate work?**

-   Called before re-rendering, allows **performance optimization**.

-   Return false to **prevent unnecessary rendering**.

js

shouldComponentUpdate(nextProps, nextState) {

return nextProps.value !== this.props.value;

}

**6. What are the different phases of the React component lifecycle?**

  **Phase**    **Description**                       **Key Methods**
  ------------ ------------------------------------- ---------------------------------------------------
  Mounting     Insert elements into DOM              constructor, render, componentDidMount
  Updating     Re-render due to state/props change   shouldComponentUpdate, render, componentDidUpdate
  Unmounting   Remove component from DOM             componentWillUnmount
  Error        Catch errors in rendering             componentDidCatch, getDerivedStateFromError

**1. Component Lifecycle (Overview)**

React component lifecycle has 3 main phases:

  **Phase**    **Description**
  ------------ -----------------------------------------------------
  Mounting     Component is created and inserted
  Updating     Component is re-rendered due to props/state changes
  Unmounting   Component is removed from DOM

**2. Class Component Lifecycle Methods**

  **Lifecycle Method**     **Phase**   **Description**
  ------------------------ ----------- --------------------------------------------------
  constructor()            Mount       Initialize state and bind methods
  componentDidMount()      Mount       Runs after component mounts (good for API calls)
  componentDidUpdate()     Update      Runs after state/props change
  componentWillUnmount()   Unmount     Cleanup before component is destroyed

**Example:**

jsx

class MyComponent extends React.Component {

constructor(props) {

super(props);

this.state = { count: 0 };

}

componentDidMount() {

console.log('Mounted');

}

componentDidUpdate() {

console.log('Updated');

}

componentWillUnmount() {

console.log('Cleanup');

}

render() {

return &lt;div&gt;{this.state.count}&lt;/div&gt;;

}

}

**3. Functional Components with Hooks**

React hooks replicate lifecycle behavior in functional components:

  **Lifecycle Equivalent**   **Hook**
  -------------------------- -----------------------------------
  componentDidMount          useEffect(..., \[\])
  componentDidUpdate         useEffect(..., \[dep\])
  componentWillUnmount       Cleanup function inside useEffect

**4. useEffect Lifecycle Mapping**

  **useEffect Setup**                                   **Lifecycle Equivalent**
  ----------------------------------------------------- ----------------------------
  useEffect(() =&gt; { ... }, \[\])                     componentDidMount
  useEffect(() =&gt; { ... }, \[dep\])                  componentDidUpdate for dep
  useEffect(() =&gt; { return () =&gt; {...} }, \[\])   componentWillUnmount

**Example:**

jsx

useEffect(() =&gt; {

console.log('Mounted');

return () =&gt; {

console.log('Cleanup');

};

}, \[\]);

**5. Cleanup Logic in Effects**

-   Useful for **clearing intervals, timeouts, event listeners,
    subscriptions**.

-   Return a function from useEffect().

**Example:**

jsx

useEffect(() =&gt; {

const interval = setInterval(() =&gt; {

console.log('Running...');

}, 1000);

return () =&gt; clearInterval(interval);

}, \[\]);

**6. Re-renders and Dependency Arrays**

  **Dependency Array**   **Behavior**
  ---------------------- --------------------------------------
  \[\]                   Run once on mount
  \[var1, var2\]         Run when any listed variable changes
  *(no array)*           Runs after every render

💡 Always define all used variables/functions in the dependency array to
avoid stale closures.
