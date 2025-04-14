**🗃️ Redux**

**1. What is Redux, and why is it used?**

Redux is a **predictable state container** for JavaScript apps, often
used with React. It helps manage the **application state** in a single
place, making it easier to debug and test.

**Why use Redux:**

-   Centralized state management

-   Predictable state changes

-   Easier debugging with tools like Redux DevTools

-   Middleware support for side effects (e.g., API calls)

**2. What are the core principles of Redux?**

  **Principle**                    **Explanation**
  -------------------------------- ---------------------------------------------------------------------------------
  **Single source of truth**       The entire state of the app is stored in one central object (store).
  **State is read-only**           The only way to change the state is by dispatching actions.
  **Changes via pure functions**   Reducers are pure functions that take state and action, and return a new state.

**3. What is the Redux store?**

The **store** is a centralized object that holds the application’s
state.

js

import { createStore } from 'redux';

const store = createStore(reducer);

It provides:

-   getState(): to read state

-   dispatch(action): to trigger updates

-   subscribe(listener): to listen for changes

**4. What are actions and reducers in Redux?**

-   **Actions**: Plain JavaScript objects with a type field that
    describe what happened.

js

const increment = { type: 'INCREMENT' };

-   **Reducers**: Pure functions that take the previous state and an
    action, and return the next state.

js

function counter(state = 0, action) {

switch (action.type) {

case 'INCREMENT':

return state + 1;

default:

return state;

}

}

**5. What is Redux Thunk, and how does it work?**

**Redux Thunk** is a middleware that allows action creators to return
**functions** instead of plain objects, useful for **async operations**
like API calls.

js

const fetchUser = () =&gt; {

return (dispatch) =&gt; {

dispatch({ type: 'FETCH\_USER\_REQUEST' });

fetch('/user')

.then(res =&gt; res.json())

.then(data =&gt; dispatch({ type: 'FETCH\_USER\_SUCCESS', payload: data
}))

.catch(error =&gt; dispatch({ type: 'FETCH\_USER\_FAILURE', error }));

};

};

**6. What is Redux Saga, and how is it different from Redux Thunk?**

**Redux Saga** is another middleware to handle side effects using
**generator functions**. It separates side-effect logic from UI logic
more cleanly.

js

import { takeEvery, call, put } from 'redux-saga/effects';

function\* fetchUserSaga() {

try {

const data = yield call(fetch, '/user');

yield put({ type: 'FETCH\_USER\_SUCCESS', payload: data });

} catch (error) {

yield put({ type: 'FETCH\_USER\_FAILURE', error });

}

}

function\* watchUser() {

yield takeEvery('FETCH\_USER\_REQUEST', fetchUserSaga);

}

  **Feature**    **Redux Thunk**         **Redux Saga**
  -------------- ----------------------- ------------------------------------
  Syntax         Uses functions          Uses generator functions
  Control Flow   Less control            More powerful control over flow
  Complexity     Simple for small apps   Better for complex async workflows

**7. How does the Context API compare to Redux?**

  **Feature**   **Context API**        **Redux**
  ------------- ---------------------- ---------------------------------------
  Use Case      Simple state sharing   Complex state management
  Boilerplate   Minimal                More setup (actions, reducers, store)
  Middleware    Not available          Rich middleware support (Thunk, Saga)
  DevTools      No built-in support    Excellent Redux DevTools
  Performance   May cause re-renders   More optimized for performance

Use **Context API** for small to medium apps and **Redux** when you need
scalable, structured state handling.

**1. Local State (useState, useReducer)**

**🧠 useState**

-   For **simple local state** (booleans, strings, numbers).

jsx

const \[count, setCount\] = useState(0);

**⚙️ useReducer**

-   For **more complex state logic**, like toggling, form updates, etc.

jsx

const reducer = (state, action) =&gt; {

switch (action.type) {

case "increment": return { count: state.count + 1 };

default: return state;

}

};

const \[state, dispatch\] = useReducer(reducer, { count: 0 });

**2. Lifting State Up**

-   Share state between sibling components by **lifting it to the
    closest common parent**.

-   Move state and handler functions **up** and pass them down via
    **props**.

jsx

// Parent

const \[value, setValue\] = useState("");

// Pass to children as props

&lt;ChildA value={value} /&gt;

&lt;ChildB setValue={setValue} /&gt;

**3. Global State Options**

When multiple components across the app need access to the same state,
use **global state** solutions like:

  **Tool**        **Use Case**
  --------------- -------------------------------------------
  Context API     Simple global state (themes, auth, user)
  Redux Toolkit   Complex, large-scale app state management

**4. Context API (createContext, useContext)**

**🔧 Steps:**

1.  **Create Context**

jsx

const UserContext = createContext();

2.  **Provide Context**

jsx

&lt;UserContext.Provider value={{ user, setUser }}&gt;

&lt;App /&gt;

&lt;/UserContext.Provider&gt;

3.  **Consume Context**

jsx

const { user } = useContext(UserContext);

✅ Great for: Theme, Auth, Language, or any small shared state.

**5. Redux (Toolkit)**

Redux Toolkit simplifies Redux setup and boilerplate.

**🔁 Key Concepts:**

  **Part**      **Description**
  ------------- ---------------------------------------
  slice         Defines state + reducers in one place
  store         Centralized state container
  useSelector   Read state from store
  useDispatch   Dispatch actions to update state

**🔧 Example:**

js

// counterSlice.js

const counterSlice = createSlice({

name: 'counter',

initialState: { value: 0 },

reducers: {

increment: state =&gt; { state.value++ }

}

});

export const { increment } = counterSlice.actions;

export default counterSlice.reducer;

js

// store.js

const store = configureStore({ reducer: { counter: counterReducer } });

jsx

// Usage

const count = useSelector(state =&gt; state.counter.value);

const dispatch = useDispatch();
