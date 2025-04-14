**🧠 1. What are Higher-Order Components (HOC)?**

A **Higher-Order Component (HOC)** is a **function** that takes a
component and returns a new enhanced component.

jsx

const withExtraInfo = (WrappedComponent) =&gt; {

return function Enhanced(props) {

return &lt;WrappedComponent {...props} extraInfo="Hello!" /&gt;;

};

};

✅ **Use Cases**:

-   Code reuse (e.g. authentication, theming)

-   Conditional rendering

-   Injecting props

🔹 Think of HOCs like decorators that wrap behavior around components.

**💾 2. Difference between localStorage, sessionStorage, and cookies**

  **Feature**        **localStorage**         **sessionStorage**         **cookies**
  ------------------ ------------------------ -------------------------- --------------------------
  Persistence        Until manually cleared   Until tab/browser closes   Custom (expiry settable)
  Capacity           \~5–10 MB                \~5 MB                     \~4 KB
  Accessible to JS   Yes                      Yes                        Yes (if not HttpOnly)
  Sent with HTTP     ❌                        ❌                          ✅ Automatically sent
  Best for           Long-term client data    Temporary data             Auth tokens, preferences

🔹 Use cookies for server-required info, and localStorage or
sessionStorage for client-only data.

**🌐 3. What is WebSockets, and how can you use it in React?**

**WebSockets** provide full-duplex communication over a single TCP
connection — great for real-time apps (chat, games, live feeds).

**Simple WebSocket in React:**

jsx

import { useEffect, useRef } from 'react';

function ChatSocket() {

const socket = useRef(null);

useEffect(() =&gt; {

socket.current = new WebSocket('ws://localhost:3000');

socket.current.onmessage = (event) =&gt; {

console.log('Message:', event.data);

};

return () =&gt; socket.current.close();

}, \[\]);

return &lt;div&gt;WebSocket Connected&lt;/div&gt;;

}

✅ Use libraries like **Socket.IO** for fallback support and better event
handling.

**🌙 4. How do you implement dark mode in a React app?**

**Basic setup using Tailwind CSS (or plain CSS):**

1.  **Toggle class on root element (like html or body):**

jsx

const toggleTheme = () =&gt; {

document.documentElement.classList.toggle('dark');

};

2.  **Set styles in Tailwind config or CSS:**

js

// tailwind.config.js

darkMode: 'class'

3.  **Persist preference:**

jsx

localStorage.setItem('theme', 'dark');

✅ You can also use useContext or Redux for global theme state.

**📱 5. What is a PWA (Progressive Web App), and how can you make a React
app a PWA?**

A **PWA** is a web app with features like:

-   Works offline

-   Installable like a native app

-   Fast & reliable performance

**Steps to convert a React app into a PWA:**

1.  **Use Create React App with PWA template:**

> bash
>
> npx create-react-app my-app --template cra-template-pwa

1.  **Register the service worker in index.js:**

> js
>
> import \* as serviceWorkerRegistration from
> './serviceWorkerRegistration';
>
> serviceWorkerRegistration.register();

1.  **Add a manifest.json:** Includes app name, icon, colors, etc.

2.  **Deploy over HTTPS** (service workers require secure context).

🧠 Tools like Lighthouse help verify PWA readiness.
