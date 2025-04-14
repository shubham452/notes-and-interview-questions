**🌐 Server-Side Rendering (SSR) and Static Site Generation (SSG)**

**1. What is Server-Side Rendering (SSR) in React?**

SSR means the **HTML is generated on the server at request time**, and
sent to the client. It improves SEO and initial load performance.

**2. How is SSR different from Client-Side Rendering (CSR)?**

  **Feature**         **SSR**                        **CSR**
  ------------------- ------------------------------ ------------------------
  Rendering           Server                         Browser
  Initial Load Time   Faster                         Slower
  SEO                 Friendly                       Less effective
  Interactivity       Delayed until JS is hydrated   Immediate after render

**3. What is Static Site Generation (SSG)?**

SSG **pre-renders pages at build time**, resulting in fast load and
great performance. Content is static unless rebuilt.

**4. What is Incremental Static Regeneration (ISR)?**

ISR allows **updating static pages after deployment** without rebuilding
the whole app.

js

export async function getStaticProps() {

return {

props: {},

revalidate: 10, // re-generates the page every 10 seconds

};

}

**5. How does Next.js support SSR, SSG, and ISR?**

  **Rendering Type**   **Method**                    **When It's Run**
  -------------------- ----------------------------- -------------------------------
  SSR                  getServerSideProps            On every request
  SSG                  getStaticProps                At build time
  ISR                  getStaticProps + revalidate   On-demand/static regeneration

**6. How do you fetch data in Next.js for SSR?**

js

export async function getServerSideProps(context) {

const res = await fetch('https://api.example.com/data');

const data = await res.json();

return { props: { data } };

}

-   Runs on **each request**

-   Great for **dynamic data**

**7. How do you fetch data in Next.js for SSG?**

js

export async function getStaticProps() {

const res = await fetch('https://api.example.com/data');

const data = await res.json();

return { props: { data } };

}

-   Runs **at build time**

-   Great for **static content** or infrequently updated data

**8. What is getServerSideProps, and when should it be used?**

-   Used for **Server-Side Rendering**

-   Runs on the **server for every request**

-   Best for **dynamic data** that changes per request

**9. What is getStaticProps, and how is it different from
getServerSideProps?**

  **Feature**   **getStaticProps**   **getServerSideProps**
  ------------- -------------------- -------------------------------
  Timing        Build time           Request time
  Use case      Static content       Dynamic or user-specific data
  Performance   Fast (cached)        Slower (real-time)

**10. What is getStaticPaths, and when is it used?**

-   Used with **dynamic routes** in SSG

-   Defines which paths should be **pre-rendered** at build time

js

export async function getStaticPaths() {

const res = await fetch('https://api.example.com/posts');

const posts = await res.json();

const paths = posts.map(post =&gt; ({

params: { id: post.id.toString() },

}));

return { paths, fallback: false };

}

Used alongside getStaticProps for dynamic routes like /posts/\[id\].
