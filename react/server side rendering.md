Sure! Here's your fully formatted and cleaned-up Markdown (`.md`) version of the **Server-Side Rendering (SSR) & Static Site Generation (SSG)** topics:

---


# 🌐 Server-Side Rendering (SSR) and Static Site Generation (SSG)

---

## ✅ 1. What is Server-Side Rendering (SSR) in React?

SSR means the **HTML is generated on the server at request time**, and sent to the client. It improves SEO and initial load performance.

---

## ✅ 2. How is SSR different from Client-Side Rendering (CSR)?

| Feature           | SSR                            | CSR                                |
|-------------------|--------------------------------|-------------------------------------|
| Rendering         | Server                         | Browser                             |
| Initial Load Time | Faster                         | Slower                              |
| SEO               | Friendly                       | Less effective                      |
| Interactivity     | Delayed until hydration        | Immediate after render              |

---

## ✅ 3. What is Static Site Generation (SSG)?

SSG **pre-renders pages at build time**, resulting in fast load and great performance. Content is static unless rebuilt.

---

## ✅ 4. What is Incremental Static Regeneration (ISR)?

ISR allows **updating static pages after deployment** without rebuilding the whole app.

```js
export async function getStaticProps() {
  return {
    props: {},
    revalidate: 10, // re-generates the page every 10 seconds
  };
}
````

---

## ✅ 5. How does Next.js support SSR, SSG, and ISR?

| Rendering Type | Method                      | When It's Run                 |
| -------------- | --------------------------- | ----------------------------- |
| SSR            | getServerSideProps          | On every request              |
| SSG            | getStaticProps              | At build time                 |
| ISR            | getStaticProps + revalidate | On-demand/static regeneration |

---

## ✅ 6. How do you fetch data in Next.js for SSR?

```js
export async function getServerSideProps(context) {
  const res = await fetch('https://api.example.com/data');
  const data = await res.json();
  return { props: { data } };
}
```

* Runs on **each request**
* Great for **dynamic data**

---

## ✅ 7. How do you fetch data in Next.js for SSG?

```js
export async function getStaticProps() {
  const res = await fetch('https://api.example.com/data');
  const data = await res.json();
  return { props: { data } };
}
```

* Runs **at build time**
* Great for **static or infrequently updated content**

---

## ✅ 8. What is `getServerSideProps`, and when should it be used?

* Used for **Server-Side Rendering**
* Runs on the **server for every request**
* Best for **dynamic data** that changes frequently

---

## ✅ 9. What is `getStaticProps`, and how is it different from `getServerSideProps`?

| Feature     | getStaticProps  | getServerSideProps       |
| ----------- | --------------- | ------------------------ |
| Timing      | Build time      | Request time             |
| Use case    | Static content  | Dynamic or user-specific |
| Performance | Faster (cached) | Slower (real-time fetch) |

---

## ✅ 10. What is `getStaticPaths`, and when is it used?

* Used with **dynamic routes** in SSG
* Defines which paths should be **pre-rendered** at build time

```js
export async function getStaticPaths() {
  const res = await fetch('https://api.example.com/posts');
  const posts = await res.json();

  const paths = posts.map(post => ({
    params: { id: post.id.toString() },
  }));

  return { paths, fallback: false };
}
```

---

## ✅ 11. ReactDOMServer API

Used for custom SSR setups (e.g., with Express.js):

```js
import express from 'express';
import ReactDOMServer from 'react-dom/server';
import App from './App';

const app = express();

app.get('*', (req, res) => {
  const html = ReactDOMServer.renderToString(<App />);
  res.send(`<html><body><div id="root">${html}</div></body></html>`);
});
```

---

## ✅ 12. Hydration

> Hydration is the process of attaching React to server-rendered HTML.

```js
ReactDOM.hydrate(<App />, document.getElementById('root'));
```

🧠 Without hydration, HTML renders but React won’t respond to events.

---

## ✅ 13. SEO Benefits of SSR

* Fully rendered HTML is crawlable
* Best for:

  * Blogs
  * Product pages
  * Marketing/landing pages
  * News and articles

---

## ✅ 14. Performance Considerations

* SSR adds **server load** and increases response time

✅ Tips:

* Cache SSR output (CDN, Redis)
* Use **Incremental Static Regeneration** when possible
* Show **loading placeholders** until hydration

---

## ✅ 15. Authentication in SSR

* Use cookies or tokens on the **server side**
* Example in Next.js:

```js
export async function getServerSideProps(context) {
  const token = context.req.cookies.token;
  if (!token) {
    return { redirect: { destination: '/login', permanent: false } };
  }
}
```

---

## ✅ 16. Styling and CSS-in-JS with SSR

✅ Choose SSR-compatible solutions:

* Emotion
* Styled-components
* MUI with `ServerStyleSheets`
* Tailwind CSS (no runtime dependency)

---

## ✅ 17. Code Splitting and Lazy Loading in SSR

✅ Use `next/dynamic` for SSR-safe dynamic imports:

```js
import dynamic from 'next/dynamic';
const Chart = dynamic(() => import('../components/Chart'), { ssr: false });
```

---

## ✅ 18. Streaming in React 18

> Improves SSR performance by **streaming HTML chunks**

```js
import { renderToPipeableStream } from 'react-dom/server';
```

Used in frameworks like Next.js App Router (React 18+).

---

## ✅ 19. Error Handling in SSR

* Handle server-side errors gracefully
* Avoid exposing stack traces
* Use `ErrorBoundary` + fallback UI

---

## ✅ 20. Client-Side Only Components

Some components rely on `window`, `document`, etc.

✅ Use `next/dynamic` to disable SSR:

```js
const NoSSRComponent = dynamic(() => import('./OnlyClient'), { ssr: false });
```

---

## ✅ 21. Deployment Concerns

* SSR requires **Node.js server** or **serverless environment**
* Ensure caching strategies (CDN, ISR)
* Deploy on Vercel, AWS Lambda, or Express server

---

## 📌 Summary Table

| Topic              | Description                                  |
| ------------------ | -------------------------------------------- |
| What is SSR        | Render React on the server                   |
| ReactDOMServer API | For manual SSR setups                        |
| Next.js            | Best framework for SSR/SSG/ISR               |
| getServerSideProps | Server-side fetch on every request           |
| Hydration          | Attaches React to server-rendered HTML       |
| SEO                | Improves search engine visibility            |
| Performance        | Tradeoff: slower backend, faster first paint |
| Authentication     | Secure SSR via cookies/token                 |
| Styling            | Use SSR-compatible libraries                 |
| Dynamic imports    | Use `next/dynamic` safely with SSR           |

---

```

Let me know if you'd like:
- A downloadable `.md` file
- A printable PDF version
- A visual **mind map**
- Or an actual **Next.js starter SSR/SSG project setup**
```
