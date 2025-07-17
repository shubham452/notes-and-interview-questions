✅ Core Topics to Know for API Handling in React
1. Fetching Data from APIs
fetch() API (vanilla JS)

axios (3rd party library)

When to use fetch vs axios

2. Using useEffect for Side Effects
Fetching data on component mount

Using dependency arrays correctly

Cleanup inside useEffect for canceling requests

3. useState + useEffect Together
Storing and displaying API data

Setting loading and error states

useEffect(() => {
  fetch('https://api.example.com/users   ')
    .then(res => res.json())
    .then(data => setUsers(data))
    .catch(err => setError(err));
}, []);
4. Error Handling
Handling network failures, server errors

Setting fallback UIs or messages

Try/catch with async/await

5. Loading Indicators
Show loading spinners while waiting for the API

Hide once data is fetched

if (loading) return <p>Loading...</p>;
6. CRUD Operations with API
Create: POST

Read: GET

Update: PUT / PATCH

Delete: DELETE

Know how to implement all 4 operations using fetch or axios.

7. Debouncing API Calls
Avoid making too many calls (e.g., on search inputs)

Use lodash’s debounce() or custom debounce function

8. Optimistic UI Updates
Update the UI before server confirms (e.g., deleting an item)

Rollback on error

9. AbortController (Cancelling Requests)
Prevent memory leaks if component unmounts before response arrives

const controller = new AbortController();
fetch(url, { signal: controller.signal });
return () => controller.abort();
10. Custom Hooks for API
useApi(), useFetch(), usePost()

DRY reusable API logic

function useFetch(url) {
  const [data, setData] = useState(null);
  useEffect(() => {
    fetch(url).then(res => res.json()).then(setData);
  }, [url]);
  return data;
}
11. Authentication APIs
Login/Signup

Storing tokens (localStorage/cookies)

Setting auth headers (Authorization: Bearer <token>)

12. Handling Protected Routes
Redirect if API returns 401

Store & check auth token before fetching

13. API Pagination
Handling paged results (?page=2)

Load more / infinite scroll / numbered pagination

14. Working with Forms & API
Controlled components + submit to API

Handle form submission and success/error states

15. API Caching & State Libraries (Advanced)
React Query / TanStack Query

SWR (stale-while-revalidate)

Benefits: cache, auto re-fetching, background sync







**🧭 React Router Notes (v6+) with Examples**

---

## ✅ React + API Integration: Full Notes with Examples

---

### 1. **Fetching Data from APIs**

Use `fetch()` or `axios` to retrieve data.

```jsx
fetch('https://api.example.com/users')
  .then(res => res.json())
  .then(data => console.log(data));
```

With axios:

```jsx
import axios from 'axios';
axios.get('/api/users').then(res => console.log(res.data));
```

---

### 2. **Using `useEffect` to Fetch on Mount**

```jsx
useEffect(() => {
  fetch('/api/data')
    .then(res => res.json())
    .then(setData);
}, []); // [] ensures it runs only once
```

---

### 3. **Managing Loading and Error State**

```jsx
const [data, setData] = useState(null);
const [loading, setLoading] = useState(true);
const [error, setError] = useState(null);

useEffect(() => {
  fetch('/api/data')
    .then(res => res.json())
    .then(setData)
    .catch(setError)
    .finally(() => setLoading(false));
}, []);
```

---

### 4. **CRUD Operations**

#### Create (POST):

```jsx
axios.post('/api/user', { name: 'Shubham' });
```

#### Update (PUT/PATCH):

```jsx
axios.put('/api/user/1', { name: 'New Name' });
```

#### Delete:

```jsx
axios.delete('/api/user/1');
```

---

### 5. **Debouncing API Calls (Search)**

```jsx
import { debounce } from 'lodash';
const search = debounce((query) => fetchData(query), 300);
```

---

### 6. **Optimistic UI Updates**

* Update UI **before** server confirms.
* Rollback if API fails.

```jsx
const handleDelete = (id) => {
  setItems(items.filter(item => item.id !== id));
  axios.delete(`/api/items/${id}`).catch(() => fetchItems());
};
```

---

### 7. **AbortController to Cancel API on Unmount**

```jsx
useEffect(() => {
  const controller = new AbortController();
  fetch('/api/data', { signal: controller.signal });
  return () => controller.abort();
}, []);
```

---

### 8. **Creating Custom API Hooks**

```jsx
function useFetch(url) {
  const [data, setData] = useState(null);
  useEffect(() => {
    fetch(url).then(res => res.json()).then(setData);
  }, [url]);
  return data;
}
```

---

### 9. **Authentication APIs**

* POST to `/login`, get token
* Store token in `localStorage`
* Send token in headers

```jsx
axios.get('/api/profile', {
  headers: { Authorization: `Bearer ${token}` },
});
```

---

### 10. **Protected Routes + Redirect on 401**

```jsx
axios.interceptors.response.use(
  res => res,
  err => {
    if (err.response.status === 401) navigate('/login');
    return Promise.reject(err);
  }
);
```

---

### 11. **Pagination from API**

```jsx
useEffect(() => {
  fetch(`/api/items?page=${page}`)
    .then(res => res.json())
    .then(setItems);
}, [page]);
```

---

### 12. **Forms and API Submission**

```jsx
const handleSubmit = (e) => {
  e.preventDefault();
  axios.post('/api/contact', { name, email, message });
};
```

---

### 13. **React Query / SWR (Advanced)**

```jsx
// React Query Example
const { data, isLoading, error } = useQuery('todos', () => axios.get('/api/todos'));
```

---

Would you like a downloadable cheatsheet for this, or an API + React project example?
