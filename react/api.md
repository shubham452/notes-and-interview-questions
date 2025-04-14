**✅ 1. How do you fetch data in React?**

You can fetch data using built-in fetch, or libraries like **Axios**,
typically inside useEffect to run it after the component mounts.

jsx

import { useEffect, useState } from \'react\';

function DataFetcher() {

const \[data, setData\] = useState(\[\]);

useEffect(() =\> {

fetch(\'https://api.example.com/items\')

.then(res =\> res.json())

.then(setData)

.catch(console.error);

}, \[\]);

return \<div\>{JSON.stringify(data)}\</div\>;

}

**✅ 2. What is the difference between fetch and Axios?**

  -----------------------------------------------------------------------
  **Feature**    **fetch**                      **Axios**
  -------------- ------------------------------ -------------------------
  Built-in       Yes (in browsers)              No (needs installation)

  Response       Manual res.json() needed       Auto parses JSON

  Error Handling Only network errors (not       Catches HTTP errors too
                 4xx/5xx)                       

  Request Cancel Manual with AbortController    Built-in with CancelToken

  Interceptors   Not available                  Available (for auth,
                                                logging)

  Upload Support Basic                          Better support for
                                                multipart
  -----------------------------------------------------------------------

**✅ 3. How do you handle errors in API calls?**

Wrap the call in try-catch (for async/await) or use .catch() with
promises.

**Example with fetch:**

jsx

useEffect(() =\> {

const fetchData = async () =\> {

try {

const res = await fetch(\'https://api.example.com/items\');

if (!res.ok) throw new Error(\'Network response was not ok\');

const json = await res.json();

setData(json);

} catch (error) {

console.error(\'Fetch error:\', error);

setError(error.message);

}

};

fetchData();

}, \[\]);

**✅ 4. What is the use of useEffect for fetching data?**

-   Ensures the data fetch runs **after component mounts**

-   Prevents side effects (like API calls) from running on every render

-   Can re-run based on dependencies (e.g., userId, searchTerm)

jsx

useEffect(() =\> {

// fetch data when component loads or when dependencies change

}, \[dependency\]);

**✅ 5. How do you handle loading states in API calls?**

Use a loading state to indicate whether the data is still being fetched.

jsx

const \[loading, setLoading\] = useState(true);

useEffect(() =\> {

const fetchData = async () =\> {

setLoading(true);

try {

const res = await fetch(\'https://api.example.com/items\');

const json = await res.json();

setData(json);

} catch (error) {

setError(error.message);

} finally {

setLoading(false);

}

};

fetchData();

}, \[\]);

**Render conditionally:**

jsx

return (

\<\>

{loading ? \<p\>Loading\...\</p\> :
\<div\>{JSON.stringify(data)}\</div\>}

\</\>

);
