**🗑️ JavaScript Garbage Collection (GC) Explained**

JavaScript automatically manages memory using **Garbage Collection (GC)**. This process frees up memory occupied by unused objects, preventing memory leaks.

-----
**📌 What is Garbage Collection?**

Garbage Collection is a process in JavaScript that **automatically removes objects from memory when they are no longer accessible**.

JavaScript uses **Reference Counting & Reachability-based Garbage Collection (Mark-and-Sweep)** to decide which objects should be removed.

-----
**📌 How Memory Works in JavaScript?**

1. **Memory Allocation:**
   1. JavaScript **allocates memory** when variables, objects, or functions are created.
1. **Memory Usage (Execution):**
   1. The allocated memory is **used during execution**.
1. **Memory Deallocation (Garbage Collection):**
   1. When objects **become unreachable**, JavaScript **frees memory** automatically.

**📌 Memory Leaks & Avoiding Them**

Even with garbage collection, **memory leaks** can still happen.

**🔴 Common Causes of Memory Leaks**

1. **Uncleared References**

   ✅ Fix: Set obj.ref = null; when it's no longer needed.

1. **Global Variables**

   ✅ Fix: Always declare variables with let, const, or var.

1. **Event Listeners Not Removed**

   ✅ Fix: Remove event listeners when not needed:

   button.removeEventListener("click", myFunction);

-----

**📌 Key Takeaways**

✅ JavaScript **automatically** manages memory with Garbage Collection.
✅ The **Mark-and-Sweep Algorithm** removes unused objects.
✅ **Memory leaks** happen if objects are not properly dereferenced.
✅ Avoid **global variables, unremoved event listeners, and detached DOM elements**.

