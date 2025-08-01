### 🌀 React Portals – Complete Guide

---

### ✅ What is a React Portal?

A **React Portal** lets you **render a child component into a DOM node that exists outside the parent component’s DOM hierarchy**.

> Think of modals, tooltips, dropdowns — you want them to break out of the normal DOM structure.

---

### 📦 Syntax

```jsx
import { createPortal } from 'react-dom';

createPortal(child, container)
```

* `child`: JSX to render
* `container`: Target DOM node (usually outside `#root`)

---

### 📌 Use Case Example: Modal with Portal

#### 1. Add portal root to `public/index.html`

```html
<!-- public/index.html -->
<body>
  <div id="root"></div>
  <div id="modal-root"></div> <!-- portal destination -->
</body>
```

#### 2. Modal component using portal

```jsx
// Modal.js
import React from 'react';
import ReactDOM from 'react-dom';

const Modal = ({ children, onClose }) => {
  return ReactDOM.createPortal(
    <div className="fixed inset-0 bg-black bg-opacity-50 flex justify-center items-center z-50">
      <div className="bg-white p-6 rounded shadow-lg relative">
        <button onClick={onClose} className="absolute top-2 right-2">❌</button>
        {children}
      </div>
    </div>,
    document.getElementById('modal-root')  // target DOM node
  );
};

export default Modal;
```

#### 3. Use it in App

```jsx
// App.js
import { useState } from 'react';
import Modal from './Modal';

function App() {
  const [showModal, setShowModal] = useState(false);

  return (
    <div className="p-6">
      <h1 className="text-xl">React Portal Example</h1>
      <button onClick={() => setShowModal(true)}>Open Modal</button>

      {showModal && (
        <Modal onClose={() => setShowModal(false)}>
          <p>This is rendered via portal!</p>
        </Modal>
      )}
    </div>
  );
}
```

---

### 🎯 Why Use Portals?

| Problem                        | Portals Solve It? |
| ------------------------------ | ----------------- |
| Modal not overlapping properly | ✅                 |
| Tooltip gets clipped in parent | ✅                 |
| Overflow / z-index issues      | ✅                 |
| DOM hierarchy restrictions     | ✅                 |

---

### 🔥 Real-World Uses

* ✅ Modals
* ✅ Toasts
* ✅ Tooltips / Dropdowns
* ✅ Context menus

---

Would you like a **complete Tailwind-based Modal Portal** with transitions?
