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

Let’s break this down clearly and simply: **Redux**, **Redux Toolkit**, and **Redux Thunk** are tools for managing **global state** in large React apps.

---

## 🧠 1. What is Redux?

Redux is a **predictable state container** for JavaScript apps.

### Core Concepts:

* **Store** – the global state of your app.
* **Actions** – plain JS objects describing “what happened.”
* **Reducers** – functions that update state based on actions.

---

### 📦 Simple Redux Example:

**Counter app**:

```tsx
// actions.js
export const increment = () => ({ type: 'INCREMENT' });
export const decrement = () => ({ type: 'DECREMENT' });

// reducer.js
const initialState = { count: 0 };

export const counterReducer = (state = initialState, action) => {
  switch (action.type) {
    case 'INCREMENT':
      return { count: state.count + 1 };
    case 'DECREMENT':
      return { count: state.count - 1 };
    default:
      return state;
  }
};

// store.js
import { createStore } from 'redux';
import { counterReducer } from './reducer';

export const store = createStore(counterReducer);
```

In your React component:

```tsx
// CounterComponent.jsx
import React from 'react';
import { useSelector, useDispatch } from 'react-redux';
import { increment, decrement } from './actions';

const Counter = () => {
  const count = useSelector((state) => state.count);
  const dispatch = useDispatch();

  return (
    <>
      <h2>{count}</h2>
      <button onClick={() => dispatch(increment())}>+</button>
      <button onClick={() => dispatch(decrement())}>-</button>
    </>
  );
};

export default Counter;
```

---

## 🚀 2. Redux Toolkit (RTK)

**Redux Toolkit** is the official, recommended way to write Redux logic. It **simplifies Redux setup** and includes useful defaults.

### Key Features:

* `configureStore()` instead of `createStore()`
* `createSlice()` to write reducers + actions together
* Built-in support for Redux Thunk

---

### ✅ RTK Version of the Counter App:

```tsx
// counterSlice.js
import { createSlice } from '@reduxjs/toolkit';

const counterSlice = createSlice({
  name: 'counter',
  initialState: { count: 0 },
  reducers: {
    increment: (state) => { state.count += 1; },
    decrement: (state) => { state.count -= 1; }
  }
});

export const { increment, decrement } = counterSlice.actions;
export default counterSlice.reducer;
```

```tsx
// store.js
import { configureStore } from '@reduxjs/toolkit';
import counterReducer from './counterSlice';

export const store = configureStore({
  reducer: { counter: counterReducer }
});
```

```tsx
// CounterComponent.jsx
import { useSelector, useDispatch } from 'react-redux';
import { increment, decrement } from './counterSlice';

const Counter = () => {
  const count = useSelector((state) => state.counter.count);
  const dispatch = useDispatch();

  return (
    <>
      <h2>{count}</h2>
      <button onClick={() => dispatch(increment())}>+</button>
      <button onClick={() => dispatch(decrement())}>-</button>
    </>
  );
};
```

✅ **Much cleaner and easier than vanilla Redux!**

---

## ⚙️ 3. Redux Thunk

### What is it?

Redux Thunk is a **middleware** that lets you write **async logic** (like API calls) inside Redux.

With Thunk, you can return a function from an action instead of just an object.

---

### 🛠 RTK + Thunk Example:

**API call to fetch user data:**

```tsx
// userSlice.js
import { createSlice, createAsyncThunk } from '@reduxjs/toolkit';
import axios from 'axios';

// async thunk
export const fetchUser = createAsyncThunk('user/fetchUser', async () => {
  const res = await axios.get('https://jsonplaceholder.typicode.com/users/1');
  return res.data;
});

const userSlice = createSlice({
  name: 'user',
  initialState: { data: null, status: 'idle' },
  reducers: {},
  extraReducers: (builder) => {
    builder
      .addCase(fetchUser.pending, (state) => { state.status = 'loading'; })
      .addCase(fetchUser.fulfilled, (state, action) => {
        state.status = 'succeeded';
        state.data = action.payload;
      })
      .addCase(fetchUser.rejected, (state) => { state.status = 'failed'; });
  }
});

export default userSlice.reducer;
```

```tsx
// store.js
import { configureStore } from '@reduxjs/toolkit';
import userReducer from './userSlice';

export const store = configureStore({
  reducer: { user: userReducer }
});
```

```tsx
// UserComponent.jsx
import { useEffect } from 'react';
import { useDispatch, useSelector } from 'react-redux';
import { fetchUser } from './userSlice';

const User = () => {
  const dispatch = useDispatch();
  const { data, status } = useSelector((state) => state.user);

  useEffect(() => {
    dispatch(fetchUser());
  }, [dispatch]);

  if (status === 'loading') return <p>Loading...</p>;
  if (status === 'failed') return <p>Error!</p>;

  return (
    <div>
      <h2>{data?.name}</h2>
      <p>{data?.email}</p>
    </div>
  );
};
```

---

## 🧾 Summary:

| Concept         | Description                                     | Tool Example                       |
| --------------- | ----------------------------------------------- | ---------------------------------- |
| **Redux**       | Manual state management with actions & reducers | `createStore`, `useSelector`, etc. |
| **RTK**         | Simplified Redux setup                          | `configureStore`, `createSlice`    |
| **Redux Thunk** | Middleware for async actions (like API calls)   | `createAsyncThunk` in RTK          |

---

Let me know if you want a full runnable project or a custom version with auth, todo, etc.
