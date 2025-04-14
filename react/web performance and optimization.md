**🚦 1. Core Web Vitals (LCP, FID, CLS)**

**Core Web Vitals** are key performance metrics by Google focused on
real user experience:

  **Metric**   **Full Form**              **Measures**                                    **Good Threshold**
  ------------ -------------------------- ----------------------------------------------- --------------------
  **LCP**      Largest Contentful Paint   Loading performance (main content load time)    ≤ 2.5 seconds
  **FID**      First Input Delay          Interactivity (time to respond to user input)   ≤ 100 ms
  **CLS**      Cumulative Layout Shift    Visual stability (avoid layout shifts)          ≤ 0.1

✅ Use Lighthouse, Web Vitals extension, or Google Search Console to
measure and monitor them.

**⚙️ 2. Service Workers & PWA Integration**

**Service Workers** are background scripts that:

-   Cache assets for offline use

-   Intercept network requests

-   Handle push notifications

**PWA Integration in React (CRA)**:

-   Use cra-template-pwa

-   Register service worker in index.js:

> js
>
> import \* as serviceWorkerRegistration from
> './serviceWorkerRegistration';
>
> serviceWorkerRegistration.register();

🔸 Makes your app installable and available offline.

**🚀 3. Prefetching & Preloading Resources**

  **Strategy**   **Purpose**                                     **When to Use**
  -------------- ----------------------------------------------- --------------------------------------------
  **Preload**    Loads resource early for **current page**       Fonts, above-the-fold images
  **Prefetch**   Loads resource in **idle time for next page**   Routes/components the user **might** visit

**Example (in HTML or Head tags):**

html

&lt;link rel="preload" href="/fonts/my-font.woff2" as="font"
type="font/woff2" crossorigin="anonymous" /&gt;

&lt;link rel="prefetch" href="/next-page.js" as="script" /&gt;

In **React Router v6+**, use:

js

&lt;Route

path="/about"

element={&lt;About /&gt;}

loader={() =&gt; import('./About')} // preloading with code-splitting

/&gt;

**🖼️ 4. Asset Optimization (SVGs, Images, Fonts)**

**🔍 SVGs:**

-   Inline small icons as components (tree-shakeable)

-   Use tools like SVGO to minify

**🖼️ Images:**

-   Use WebP/AVIF formats for compression

-   Lazy load images (loading="lazy")

-   Serve responsive images via srcset

**🔤 Fonts:**

-   Use font-display: swap; in CSS

-   Subset only used characters (e.g., Google Fonts with text= param)

🔸 Prefer icon fonts or SVGs over raster images for scalable UI elements.

**🧵 5. Web Workers for Background Tasks**

**Web Workers** allow you to run CPU-heavy tasks without blocking the
main thread.

**Use cases:**

-   Image compression

-   Parsing large datasets

-   Calculations (e.g. crypto, math-heavy logic)

**Basic Web Worker setup:**

js

// worker.js

self.onmessage = (e) =&gt; {

const result = heavyCalculation(e.data);

self.postMessage(result);

};

js

// In React

const worker = new Worker(new URL('./worker.js', import.meta.url));

worker.postMessage(data);

worker.onmessage = (e) =&gt; {

console.log("Result from worker:", e.data);

};

🔹 Tools like **Comlink** or **Workerize** simplify usage in modern apps.
