# 🔁 Redux vs Redux Toolkit vs Redux Thunk vs Redux Saga

| **Feature**         | **Redux**                          | **Redux Toolkit (RTK)**             | **Redux Thunk**                         | **Redux Saga**                                       |
|---------------------|------------------------------------|-------------------------------------|------------------------------------------|------------------------------------------------------|
| **Type**            | State management library           | Abstraction over Redux              | Redux middleware                         | Redux middleware                                     |
| **Purpose**         | Centralized state container        | Simplify Redux setup                | Handle async logic (like API calls)      | Handle complex side-effects via generator functions |
| **Boilerplate**     | ✅ High                            | ❌ Minimal                          | Medium                                   | Medium                                               |
| **Async Handling**  | ❌ Manual                          | ✅ `createAsyncThunk`               | ✅ Built-in                              | ✅ Built-in                                          |
| **Learning Curve**  | Medium                             | Easy                                | Easy                                     | Hard                                                 |
| **Code Style**      | Manual actions + reducers          | Auto-sliced reducers/actions        | Async logic via plain functions          | Async flow via generator/yield                      |
| **Best For**        | Custom solutions & full control    | Most real-world Redux use cases     | Basic async tasks (API calls)            | Advanced side-effects (cancel, debounce, retry...)  |
| **DevTools Support**| ✅                                  | ✅                                   | ✅                                       | ✅                                                   |

---

## 📘 Redux – Core Concepts

### 🔹 What is Redux?

Redux is a **predictable state container** for managing global app state.

### 🔹 Core Principles

| Principle              | Description                                                                 |
|------------------------|-----------------------------------------------------------------------------|
| Single source of truth | The state lives in one centralized object (`store`)                         |
| State is read-only     | You change state by dispatching actions                                     |
| Pure functions         | State changes are handled by **reducers**, which are pure functions         |

---

### 🔹 Store, Actions, Reducers

```js
// Action
const increment = { type: 'INCREMENT' };

// Reducer
function counter(state = 0, action) {
  switch (action.type) {
    case 'INCREMENT':
      return state + 1;
    default:
      return state;
  }
}

// Store
import { createStore } from 'redux';
const store = createStore(counter);
🔁 Redux Thunk
🔹 What is it?
Redux Thunk is middleware that lets action creators return functions instead of plain objects.

js
Copy
Edit
const fetchUser = () => {
  return async (dispatch) => {
    dispatch({ type: 'FETCH_USER_REQUEST' });

    try {
      const res = await fetch('/user');
      const data = await res.json();
      dispatch({ type: 'FETCH_USER_SUCCESS', payload: data });
    } catch (err) {
      dispatch({ type: 'FETCH_USER_FAILURE', error: err });
    }
  };
};
🧬 Redux Saga
🔹 What is it?
Redux Saga is middleware for managing complex side-effects using generator functions.

js
Copy
Edit
import { takeEvery, call, put } from 'redux-saga/effects';

function* fetchUserSaga() {
  try {
    const data = yield call(() => fetch('/user').then(res => res.json()));
    yield put({ type: 'FETCH_USER_SUCCESS', payload: data });
  } catch (error) {
    yield put({ type: 'FETCH_USER_FAILURE', error });
  }
}

function* watchUser() {
  yield takeEvery('FETCH_USER_REQUEST', fetchUserSaga);
}
🔹 Thunk vs Saga
Feature	Redux Thunk	Redux Saga
Syntax	Async via functions	Async via generator functions (yield)
Control	Less control	More advanced control (cancel, retry, etc.)
Best For	Simple API calls	Complex async workflows
Learning Curve	Easier	Steeper

🧠 Redux Toolkit (RTK)
🔹 What is it?
RTK is the official, opinionated abstraction over Redux to reduce boilerplate and simplify setup.

🔹 Features
createSlice – Combines reducers + actions

configureStore – Auto sets up Redux DevTools and middleware

createAsyncThunk – Simplified async actions

🔹 Example
js
Copy
Edit
// counterSlice.js
import { createSlice } from '@reduxjs/toolkit';

const counterSlice = createSlice({
  name: 'counter',
  initialState: { value: 0 },
  reducers: {
    increment: (state) => { state.value += 1; },
  },
});

export const { increment } = counterSlice.actions;
export default counterSlice.reducer;
js
Copy
Edit
// store.js
import { configureStore } from '@reduxjs/toolkit';
import counterReducer from './counterSlice';

const store = configureStore({
  reducer: { counter: counterReducer }
});
js
Copy
Edit
// Usage in component
const count = useSelector((state) => state.counter.value);
const dispatch = useDispatch();
⚙️ Local vs Global State
🔹 Local State (useState, useReducer)
Tool	Use Case
useState	Simple UI state (input, toggle)
useReducer	Complex logic (forms, toggle logic)

js
Copy
Edit
const reducer = (state, action) => {
  switch (action.type) {
    case "increment": return { count: state.count + 1 };
    default: return state;
  }
};
const [state, dispatch] = useReducer(reducer, { count: 0 });
🔹 Lifting State Up
Lift state to a common parent to share across siblings.

jsx
Copy
Edit
const [value, setValue] = useState("");

<ChildA value={value} />
<ChildB setValue={setValue} />
🔹 Global State Options
Tool	Best Use Case
Context API	Simple global state (auth, theme)
Redux Toolkit	Complex global state management

🔌 Context API (Simple Global State)
js
Copy
Edit
// 1. Create
const UserContext = createContext();

// 2. Provide
<UserContext.Provider value={{ user, setUser }}>
  <App />
</UserContext.Provider>

// 3. Consume
const { user } = useContext(UserContext);
✅ Great for: Theme, Auth, Language
❌ Avoid for: Complex state flows, performance-sensitive apps

✅ Summary
Tool	Best For
Redux	Full control and customization
Redux Toolkit	Real-world apps with simplified setup
Redux Thunk	Basic async logic like API requests
Redux Saga	Complex async workflows (debounce, cancel, retry)
Context API	Lightweight shared state like theme/auth
useReducer	Local, complex component logic (form, toggle groups)
