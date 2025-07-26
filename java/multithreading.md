Here is a content page for the video, outlining the topics and subtopics, along with a list of key concepts that are important to remember:

### **Video Content Page: Java Multithreading**

*   **Introduction to Java Multithreading & Core Concepts**
    *   **CPU (Central Processing Unit)**
    *   **Core (Processing Unit)**
    *   **Program (Set of Instructions)**
    *   **Process (Instance of a Program)**
    *   **Thread (Smallest Unit of Execution)**

*   **Multitasking**
    *   **Definition**
    *   **Multitasking on Single Core CPU (Time-Sharing / Rapid Switching)**
    *   **Multitasking on Multi-Core CPU (True Parallel Execution)**
    *   **Efficiency Benefits**

*   **Multithreading vs. Multitasking**
    *   **Multithreading Definition**
    *   **Relationship and Enhancement**
    *   **Level of Operation (Process vs. Thread)**
    *   **Resource Management Differences**
    *   **Real-life Examples**

*   **Java Multithreading Fundamentals**
    *   **JVM and OS Role in Multithreading**
    *   **Main Thread**
    *   **Thread Creation in Java**
        *   **Extending `Thread` Class**
        *   **Implementing `Runnable` Interface**
        *   **Choosing Between `Thread` and `Runnable`**

*   **Thread Life Cycle (States of a Thread)**
    *   **New**
    *   **Runnable** (Ready to run / Executing)
    *   **Running** (Implicit, part of Runnable in Java's enum)
    *   **Blocked / Waiting**
    *   **Time Waiting**
    *   **Terminated**

*   **Common Thread Methods**
    *   `start()`
    *   `run()`
    *   `sleep()`
    *   `join()`
    *   `setPriority()` / `getPriority()`
    *   `setName()` / `getName()`
    *   `interrupt()`
    *   `yield()`
    *   `setDaemon()`
        *   **User Threads vs. Daemon Threads**

*   **Synchronization**
    *   **Problem Without Synchronization**
    *   **Race Condition**
    *   **Critical Section**
    *   **`synchronized` Keyword**
        *   **Mutual Exclusion**
        *   **`synchronized` Method**
        *   **`synchronized` Block**
    *   **Importance of Re-interrupting `InterruptedException`**

*   **Locks (Explicit Locking)**
    *   **Intrinsic Locks vs. Explicit Locks**
    *   **`java.util.concurrent.locks.Lock` Interface**
    *   **`ReentrantLock`**
        *   `lock()`
        *   `tryLock()`
        *   `tryLock(long timeout, TimeUnit unit)`
        *   `unlock()` (Always in `finally` block)
        *   **Reentrancy Concept**
        *   **Interruptible Locks (`lockInterruptibly()`)**
        *   **Fairness (Fair vs. Unfair Locks)**
        *   **Advantages over `synchronized`**
    *   **`ReadWriteLock`**
        *   **`ReentrantReadWriteLock`**
        *   **Multiple Readers, Exclusive Writer Principle**

*   **Deadlock**
    *   **Definition**
    *   **Four Conditions**
    *   **Resolution Strategy (Consistent Lock Acquisition Order)**

*   **Thread Communication**
    *   **Problem Without Communication (Busy Waiting)**
    *   **`wait()` Method**
    *   **`notify()` Method**
    *   **`notifyAll()` Method**
    *   **Requirement: `synchronized` Context**
    *   **Producer-Consumer Example**

*   **Thread Safety**
    *   **Definition**

*   **Lambda Expressions (Java 8 Feature)**
    *   **Simplifying Thread Creation**
    *   **Functional Interface**
    *   **Anonymous Function Concept**
    *   **Syntax and Simplifications**
    *   **Effectively Final Variables**

*   **Executors Framework & Thread Pools**
    *   **Problems Without Thread Pools**
    *   **Benefits of Thread Pools**
    *   **Core Interfaces**
        *   `Executor`
        *   `ExecutorService`
        *   `ScheduledExecutorService`
    *   **`Executors` Utility Class (Thread Pool Factories)**
        *   `newFixedThreadPool()`
        *   `newSingleThreadExecutor()`
        *   `newCachedThreadPool()`
        *   `newScheduledThreadPool()`
    *   **`ExecutorService` Methods**
        *   `submit(Runnable)`
        *   `submit(Callable)`
        *   `submit(Runnable, result)`
        *   `shutdown()`
        *   `shutdownNow()`
        *   `awaitTermination()`
        *   `isShutdown()`
        *   `isTerminated()`
    *   **`Future` Interface**
        *   `get()`
        *   `get(timeout)`
        *   `isDone()`
        *   `isCancelled()`
        *   `cancel()`
    *   **Callable vs. Runnable**
    *   **Batch Task Execution with `ExecutorService`**
        *   `invokeAll()`
        *   `invokeAll(timeout)`
        *   `invokeAny()`
        *   `invokeAny(timeout)`

*   **`ScheduledExecutorService`**
    *   **`schedule()` (One-time delayed task)**
    *   **`scheduleAtFixedRate()` (Periodic fixed-rate execution)**
    *   **`scheduleWithFixedDelay()` (Periodic fixed-delay execution)**

*   **Concurrency Utilities (Advanced Synchronization)**
    *   **`CountDownLatch`**
        *   **Purpose and Usage**
        *   **`countDown()` and `await()` Methods**
        *   **Limitation (Not Reusable)**
    *   **`CyclicBarrier`**
        *   **Purpose and Usage (Reusable Barrier)**
        *   **`await()` Method**
        *   **`reset()` Method**
        *   **Barrier Action**

*   **`CompletableFuture` (Java 8 Asynchronous Programming)**
    *   **Asynchronous Programming Concept**
    *   **`supplyAsync()`**
    *   **`get()` vs. `join()` (Checked vs. Unchecked Exceptions)**
    *   **`getNow()`**
    *   **`allOf()`**
    *   **`thenApply()`**
    *   **Error Handling (`exceptionally()`)**
    *   **Timeouts**
    *   **Controlling Thread Pool for Execution**

---

### **Key Topics to Remember**

To truly grasp Java Multithreading and succeed in real-world applications and interviews, the video emphasizes remembering these core concepts:

*   **Fundamental Distinction of Thread:** Understand that a **thread is the smallest unit of execution within a process, capable of independent operation while sharing resources.** This is key to understanding concurrent execution.
*   **Multitasking vs. Multithreading:** Clearly differentiate these. **Multitasking is about running multiple *processes* concurrently, while multithreading is about running multiple *threads within a single process* concurrently.** Multithreading enhances multitasking.
*   **Thread Life Cycle:** Be familiar with the different states (New, Runnable, Blocked/Waiting, Terminated) and what causes a thread to move between them, especially **Time Waiting (e.g., `sleep()`)** and **Blocked/Waiting** (e.g., waiting for a lock).
*   **Thread Creation Methods (`Thread` vs. `Runnable`):** Know both ways to create threads. Most importantly, **understand *when* to use `Runnable` (e.g., when your class already extends another class, or for better separation of concerns)**.
*   **Core Thread Methods:** Memorize the purpose of `start()` (creates and starts a new thread), `run()` (contains thread's logic), `sleep()` (pauses execution, throws `InterruptedException`), `join()` (waits for a thread to die), and `setDaemon()` (JVM does not wait for daemon threads to finish).
*   **Synchronization and Race Conditions:** This is a **most important topic**. Understand that **Race Conditions** occur when multiple threads access and modify shared data concurrently, leading to unpredictable results. **Synchronization (using `synchronized` keyword or `Lock` objects) is crucial to ensure only one thread enters a Critical Section at a time (Mutual Exclusion)**.
*   **Explicit Locks (`ReentrantLock`):** Understand the **advantages of `ReentrantLock` over the `synchronized` keyword**. Key benefits include **more control**, the ability for **interruptible waiting for locks (`lockInterruptibly()`), explicit fairness options, and support for `ReadWriteLock`**. Always call `unlock()` in a `finally` block.
*   **Deadlock:** Be able to **define deadlock** (threads blocked waiting for each other) and, crucially, **know the primary strategy to prevent it: consistent lock acquisition order**.
*   **Thread Communication (`wait()`, `notify()`, `notifyAll()`):** Understand why these are essential to avoid **busy waiting** and to enable efficient communication between threads (e.g., Producer-Consumer problem). **Remember they must be called within a `synchronized` block.**
*   **Thread Safety:** Grasp the fundamental definition: **A component is thread-safe if it guarantees correct behavior even when accessed by multiple threads concurrently, without data corruption or unexpected results.**
*   **Executors Framework (Thread Pools):** This is **how multithreading is primarily done in production code**. Understand the **benefits of thread pools (resource management, performance, control)**. Be familiar with different pool types (`Fixed`, `Single`, `Cached` - especially `Cached` for variable/short-lived tasks).
*   **`ExecutorService` and `Future`:** Know how to **submit tasks** (`Runnable` for no return, `Callable` for a return value) and use the `Future` object to **manage the result and status of asynchronous computations** (`get()`, `isDone()`, `cancel()`).
*   **`ScheduledExecutorService`:** Understand its purpose for **delayed and periodic task execution**. Crucially, know the difference between **`scheduleAtFixedRate` (runs at fixed intervals regardless of task duration)** and **`scheduleWithFixedDelay` (delay between task *completions*)**.
*   **Concurrency Utilities (`CountDownLatch` & `CyclicBarrier`):**
    *   **`CountDownLatch`:** Use for **one-time waiting for a set of operations to complete** (e.g., waiting for initialization services). Remember it's **not reusable**.
    *   **`CyclicBarrier`:** Use for **reusable synchronization where a group of threads wait for each other to reach a common point**.
*   **`CompletableFuture` (Java 8):** This is the **modern approach to asynchronous programming**. Understand its non-blocking nature and how it simplifies chaining and combining asynchronous operations. Know basic methods like `supplyAsync()`, `join()`, and `allOf()`.

The speaker strongly emphasizes that understanding these concepts means you've learned what a Java developer does at a production level and that these topics cover 99% of interview questions and practical work.

Here are detailed notes and coding examples on Java Multithreading, drawing directly from the provided sources:

---

### Understanding the Basics of Computer Processing

Before diving into Java Multithreading, it's essential to understand fundamental concepts of how programs run on a computer.

*   **CPU (Central Processing Unit)**: The CPU is considered the **"brain of the computer"**. Any instructions or statements written in a program (like arithmetic logic, if-else conditions) are executed inside the CPU. Examples of CPUs include Intel and AMD.
*   **Core**: A core is an **individual processing unit within a CPU**. Historically, CPUs had only one core, but now they have multiple cores (e.g., Quad-core means four cores). The actual work within the CPU happens inside the cores. More cores generally lead to better performance. Multiple cores allow multiple tasks to be processed simultaneously.
*   **Program**: A program is simply a **set of instructions** designed to perform a specific task. High-level examples include Microsoft Word or OS Studio.
*   **Process**: A process is an **"instance of a program"**. When a program starts running, the operating system (OS) initiates a corresponding process. For example, when you open Microsoft Word, the OS starts a process for it. A process consumes resources like CPU time and memory.
*   **Thread**: A thread is the **"smallest unit of execution within a process"**. A single process can contain multiple threads. These threads within a process share some resources but can run independently. For instance, in Microsoft Word, typing, spell-checking, and auto-saving can all run as separate threads within the same Word process. Similarly, a web browser like Google Chrome can use multiple threads for different tabs, as each tab can operate independently. Threads allow different parts of a program to execute concurrently.

---

### Multitasking vs. Multithreading

These are crucial concepts for understanding concurrent execution.

*   **Multitasking**:
    *   **Definition**: Multitasking allows an **operating system to run multiple processes simultaneously**. This means you can have several programs open and running at the same time on your computer, like a browser, OBS Studio, and a presentation.
    *   **How it works (Single-core CPU)**: On a single-core CPU, true simultaneous execution isn't possible. Instead, the OS rapidly switches between tasks (processes) using a technique called **"time-sharing"** or **"rapid switching between tasks"**. This rapid switching creates the *illusion* that all tasks are running concurrently. The OS scheduler manages this by allocating small time slices to each task.
    *   **How it works (Multi-core CPU)**: On multi-core CPUs, **true parallel execution occurs**. The OS scheduler distributes different tasks (processes) across multiple cores, leading to more efficient execution.
    *   **Level of Operation**: Multitasking operates at a **higher level**, dealing with the execution of multiple *processes*. Processes are the OS's primary unit of execution.
    *   **Resource Management**: Involves managing resources between **completely separate programs**, which may have different memory spaces and system resources.
    *   **Example**: Browsing the internet while listening to music and downloading files simultaneously.
    *   **Real-life Analogy**: An office manager assigning different employees (processes) to work on different projects simultaneously. Each employee works independently on their project.

*   **Multithreading**:
    *   **Definition**: Multithreading refers to the **ability to execute multiple threads within a *single process* concurrently**.
    *   **Relationship with Multitasking**: Multithreading **enhances the efficiency of multitasking**. Multitasking (multiple processes) is made better because each process itself can have multiple threads executing simultaneously. It's a more "granular" or detailed level of concurrency.
    *   **How it works**: By breaking down individual tasks into smaller sub-tasks (threads), these threads can be processed simultaneously, making better use of CPU capabilities.
    *   **Level of Operation**: Multithreading operates at a **lower, more granular level**, dealing with multiple *threads* within the *same application or process*. Threads are the smallest unit of execution within a process.
    *   **Resource Management**: Focuses on resource management *within a single process*. Threads within the same process often share memory and resources.
    *   **Example**: A web browser using separate threads for rendering a page, running JavaScript, and managing user inputs, which makes the browser more responsive and efficient.
    *   **Real-life Analogy**: Within one project (process) assigned by the office manager, a team (process) might have several employees (threads) working concurrently on different parts of that *single* project.

---

### Java Multithreading: Core Concepts & Implementation

Java provides built-in support for multithreading to maximize CPU utilization by enabling the concurrent execution of two or more threads.

*   **Java's Support**: Java's multithreading capabilities are part of the `java.lang` package, making concurrent execution easy to implement.
*   **JVM's Role**:
    *   **Single-core Environment**: In a single-core environment, Java's multithreading is managed by the Java Virtual Machine (JVM) and the OS. They switch between threads using time-slicing to give the *illusion* of concurrency. Threads share the single core.
    *   **Multi-core Environment**: In a multi-core environment, the JVM can distribute threads across multiple cores, allowing for **true parallel execution**.
*   **Main Thread**: When a Java program starts, **one thread begins running immediately, called the "main thread"**. This thread is responsible for executing the `main` method of the program. Initially, all our code runs on this single main thread.

#### Creating New Threads in Java

There are two primary ways to create new threads (in addition to the main thread) in Java:

1.  **Extending the `Thread` Class**:
    *   **Steps**:
        1.  Create a new class that **extends `java.lang.Thread`**.
        2.  **Override the `run()` method** in your new class. The code you want to execute in the new thread should be placed inside this `run()` method.
        3.  In your `main` method (or another thread), create an **object (instance) of your custom thread class**.
        4.  Call the **`start()` method** on your thread object. This method signals the JVM to create a new execution thread and call its `run()` method. **Do NOT directly call `run()`**, as it will execute in the current thread instead of a new one.

    *   **Code Example (Extending `Thread`):**
        ```java
        // File: World.java (or inner class for simplicity)
        class World extends Thread {
            @Override
            public void run() {
                for (int i = 0; i < 100000; i++) {
                    System.out.println(Thread.currentThread().getName() + ": World");
                }
            }
        }

        // File: Test.java (Main class)
        public class Test {
            public static void main(String[] args) throws InterruptedException {
                // Main thread's task
                for (int i = 0; i < 100000; i++) {
                    System.out.println(Thread.currentThread().getName() + ": Hello");
                }

                // Create and start a new thread
                World worldThread = new World(); // Object created for the new thread
                worldThread.start(); // This calls the run() method in a new thread

                // Output will show "Hello" and "World" printed randomly/interleaved
                // demonstrating concurrent execution
            }
        }
        ```
        *Self-correction:* The original source demonstrates printing `Thread.currentThread().getName()` to show different thread names. I'll add that for clarity.

2.  **Implementing the `Runnable` Interface**:
    *   **Why use `Runnable`?**: Java does not support multiple inheritance. If your class already extends another class, you cannot extend `Thread` directly. In such cases, implementing `Runnable` is the solution.
    *   **Steps**:
        1.  Create a new class that **implements `java.lang.Runnable`**.
        2.  **Override the `run()` method**. The code for the new thread goes here.
        3.  Create an **object of your custom `Runnable` class**.
        4.  Create a **`Thread` object**, passing your `Runnable` instance to its constructor.
        5.  Call the **`start()` method** on the `Thread` object.

    *   **Code Example (Implementing `Runnable`):**
        ```java
        // File: WorldRunnable.java (or inner class for simplicity)
        class WorldRunnable implements Runnable {
            @Override
            public void run() {
                for (int i = 0; i < 100000; i++) {
                    System.out.println(Thread.currentThread().getName() + ": World");
                }
            }
        }

        // File: Test.java (Main class)
        public class Test {
            public static void main(String[] args) {
                // Main thread's task
                for (int i = 0; i < 100000; i++) {
                    System.out.println(Thread.currentThread().getName() + ": Hello");
                }

                // Create Runnable instance
                WorldRunnable runnableTask = new WorldRunnable();

                // Create Thread object, passing Runnable
                Thread t1 = new Thread(runnableTask);
                t1.start(); // Start the new thread

                // Output will again show "Hello" and "World" interleaved
            }
        }
        ```

---

### Thread Life Cycle (States)

A thread can go through various states during its execution.

1.  **New**:
    *   **Description**: A thread is in this state when its **object has been created**, but the `start()` method has not yet been called. It exists but is not yet eligible to run.
    *   **Code Example**: `MyThread t1 = new MyThread();`

2.  **Runnable**:
    *   **Description**: After the `start()` method is called, the thread becomes runnable. It is **ready to run and is waiting for CPU time**. It might be currently executing or just waiting for its turn. Java internally treats "Running" as part of "Runnable".
    *   **Code Example**: `t1.start();` (after this call, `t1.getState()` might return `RUNNABLE`)

3.  **Running**:
    *   **Description**: The thread is in this state **when it is actively executing** on the CPU. As mentioned, Java's `Thread.State` enum does not explicitly have a `RUNNING` state; it's considered part of `RUNNABLE`. A thread transitions from `RUNNABLE` to actually `RUNNING` when the OS scheduler allocates CPU time to it.

4.  **Blocked / Waiting / Timed Waiting**:
    *   **Description**: A thread enters this state when it is temporarily **inactive or paused**.
        *   **Blocked**: A thread might be blocked if it's waiting to acquire a monitor lock (e.g., trying to enter a `synchronized` block that's already held by another thread).
        *   **Waiting**: A thread might be waiting indefinitely for another thread to perform a particular action (e.g., calling `Object.wait()` without a timeout).
        *   **Timed Waiting**: A thread is in this state when it is waiting for a specified amount of time (e.g., `Thread.sleep(long millis)`, `Object.wait(long millis)`, `Thread.join(long millis)`). The `Thread.sleep()` method puts a thread into a `TIMED_WAITING` state.
    *   **Code Example (Illustrating `RUNNABLE` and `TIMED_WAITING`):**
        ```java
        import java.util.concurrent.TimeUnit; // For TimeOutException
        import java.util.concurrent.locks.Lock;
        import java.util.concurrent.locks.ReentrantLock;

        class MyThread extends Thread {
            private Lock lock = new ReentrantLock();

            public MyThread(String name) {
                super(name);
            }

            @Override
            public void run() {
                try {
                    // Simulate work for 2 seconds
                    Thread.sleep(2000); // Enters TIMED_WAITING state
                    System.out.println(getName() + " finished its sleep.");
                } catch (InterruptedException e) {
                    System.out.println(getName() + " was interrupted while sleeping.");
                    Thread.currentThread().interrupt(); // Restore interrupt status
                }
            }

            // Example to show BLOCKING state (not explicitly covered by MyThread.run)
            public void acquireLockAndBlock() {
                lock.lock(); // This will block if lock is not available
                try {
                    System.out.println(getName() + " acquired lock.");
                } finally {
                    lock.unlock();
                }
            }
        }

        public class ThreadStates {
            public static void main(String[] args) throws InterruptedException {
                MyThread t1 = new MyThread("WorkerThread");

                // State 1: NEW
                System.out.println("State of WorkerThread after creation: " + t1.getState()); // Output: NEW

                t1.start(); // Moves to RUNNABLE state

                // State 2: RUNNABLE (or Running - Java's internal representation)
                // We add a small delay to give JVM a chance to schedule t1
                Thread.sleep(100);
                System.out.println("State of WorkerThread after start() call: " + t1.getState()); // Output: RUNNABLE

                // State 3: TIMED_WAITING (due to sleep in run method)
                // Wait for t1 to start sleeping
                Thread.sleep(500); // Give t1 a chance to enter sleep
                System.out.println("State of WorkerThread during sleep: " + t1.getState()); // Output: TIMED_WAITING

                // Example of Blocking state (Conceptual, needs two threads trying to acquire same lock)
                // If t1 holds a synchronized block/lock, and t2 tries to enter it, t2 will be BLOCKED
                // The provided source doesn't show a direct simple example of BLOCKED state with `getState()`
                // but explains the concept with ReentrantLock later.
                // For demonstration, if MyThread had a synchronized method and another thread called it while t1 was inside.
            }
        }
        ```

5.  **Terminated**:
    *   **Description**: A thread enters this state when it has **finished executing** its `run()` method or has been abruptly terminated. It's no longer alive.
    *   **Code Example (Illustrating `TERMINATED` state using `join()`):**
        ```java
        // ... (MyThread class as defined above) ...

        public class ThreadStates {
            public static void main(String[] args) throws InterruptedException {
                MyThread t1 = new MyThread("WorkerThread");

                System.out.println("State of WorkerThread after creation: " + t1.getState());

                t1.start();
                Thread.sleep(100); // Let it become runnable/running
                System.out.println("State of WorkerThread after start() call: " + t1.getState());

                // Main thread waits for t1 to finish execution
                t1.join(); // Main thread blocks until t1 terminates

                // State 4: TERMINATED
                System.out.println("State of WorkerThread after join() (should be terminated): " + t1.getState()); // Output: TERMINATED
            }
        }
        ```

---

### Important Thread Methods

Java's `Thread` class provides several methods to control and interact with threads.

1.  **`start()`**:
    *   **Purpose**: Initiates the execution of the thread. It calls the thread's `run()` method in a newly created execution thread. It's essential to call `start()` and *not* `run()` directly for multithreading.
    *   **Example**: `myThreadObject.start();`

2.  **`run()`**:
    *   **Purpose**: Contains the code that will be executed by the new thread. This method is overridden when extending `Thread` or implementing `Runnable`.
    *   **Example**: (See previous examples for `World` and `WorldRunnable` classes)

3.  **`sleep(long millis)`**:
    *   **Purpose**: Causes the **current thread** to pause its execution for a specified number of milliseconds. During this time, the thread enters the `TIMED_WAITING` state. It's a static method, so `Thread.sleep()`. It can throw an `InterruptedException`, which is a checked exception and must be handled.
    *   **Example**:
        ```java
        // In a thread's run() method or main method
        try {
            System.out.println(Thread.currentThread().getName() + " is going to sleep for 1 second.");
            Thread.sleep(1000); // Pause for 1000 milliseconds
            System.out.println(Thread.currentThread().getName() + " woke up.");
        } catch (InterruptedException e) {
            System.out.println(Thread.currentThread().getName() + " was interrupted while sleeping.");
            Thread.currentThread().interrupt(); // Re-interrupt the current thread
        }
        ```

4.  **`join()`**:
    *   **Purpose**: The calling thread (e.g., the `main` thread) will **wait for the thread on which `join()` is called to terminate (finish its execution)** before proceeding. This ensures sequential execution of tasks where one task depends on another's completion.
    *   **Example**:
        ```java
        // Assuming MyThread is defined as before
        public class JoinExample {
            public static void main(String[] args) throws InterruptedException {
                MyThread t1 = new MyThread("JoinThread");
                t1.start(); // Start the thread that will run for 5 seconds

                try {
                    t1.join(); // Main thread waits for t1 to complete
                } catch (InterruptedException e) {
                    System.out.println("Main thread interrupted while waiting for JoinThread.");
                    Thread.currentThread().interrupt();
                }
                System.out.println("Hello from Main after JoinThread finished."); // This will print AFTER t1 completes
            }
        }
        ```

5.  **`setPriority(int newPriority)` / `getPriority()`**:
    *   **Purpose**: Sets or retrieves the **priority** of a thread. Thread priorities range from `Thread.MIN_PRIORITY` (1) to `Thread.MAX_PRIORITY` (10), with `Thread.NORM_PRIORITY` (5) being the default.
    *   **Behavior**: Setting priority is merely a **"hint" to the OS scheduler**. It does not guarantee that higher-priority threads will always run before lower-priority ones. The actual scheduling depends on the OS and JVM implementation. Priorities are more noticeable on single-core processors.
    *   **Example**:
        ```java
        class PriorityThread extends Thread {
            public PriorityThread(String name, int priority) {
                super(name);
                setPriority(priority); // Set thread priority
            }

            @Override
            public void run() {
                for (int i = 0; i < 50000; i++) { // More iterations to make priority effect more visible
                    // Simulate some work
                    String s = "dummy";
                    for (int j = 0; j < 1000; j++) {
                        s += " " + j;
                    }
                    if (i % 10000 == 0) { // Print less frequently
                        System.out.println(getName() + " (Priority: " + getPriority() + ") - Count: " + i);
                    }
                }
            }
        }

        public class PriorityExample {
            public static void main(String[] args) throws InterruptedException {
                PriorityThread low = new PriorityThread("LowPriorityThread", Thread.MIN_PRIORITY); // Priority 1
                PriorityThread medium = new PriorityThread("MediumPriorityThread", Thread.NORM_PRIORITY); // Priority 5
                PriorityThread high = new PriorityThread("HighPriorityThread", Thread.MAX_PRIORITY); // Priority 10

                low.start();
                medium.start();
                high.start();

                // Join to wait for all threads to complete
                low.join();
                medium.join();
                high.join();
            }
        }
        ```

6.  **`setName(String name)` / `getName()`**:
    *   **Purpose**: Assigns a custom name to a thread or retrieves its name. This is useful for debugging and logging.
    *   **Example**: (See `PriorityThread` constructor and `System.out.println` statements above)

7.  **`interrupt()`**:
    *   **Purpose**: Interrupts the thread on which this method is called. It sets the thread's interrupt status to `true`. If the thread is currently in a `sleep()`, `wait()`, or `join()` state, it will throw an `InterruptedException` and clear its interrupt status. It's a way to signal a thread to stop what it's doing.
    *   **Important**: The `InterruptedException` must be caught, and typically the thread's interrupt status should be restored (`Thread.currentThread().interrupt();`) to propagate the interruption signal.
    *   **Example**:
        ```java
        class InterruptibleThread extends Thread {
            public InterruptibleThread(String name) {
                super(name);
            }

            @Override
            public void run() {
                try {
                    System.out.println(getName() + " is going to sleep for 5 seconds.");
                    Thread.sleep(5000); // Will be interrupted
                    System.out.println(getName() + " woke up completely."); // This might not print
                } catch (InterruptedException e) {
                    System.out.println(getName() + ": Interrupted while sleeping! Message: " + e.getMessage());
                    Thread.currentThread().interrupt(); // Restore the interrupted status
                }
                System.out.println(getName() + " finished execution."); // This will print after interruption
            }
        }

        public class InterruptExample {
            public static void main(String[] args) throws InterruptedException {
                InterruptibleThread t1 = new InterruptibleThread("MyInterruptibleThread");
                t1.start();

                // Main thread sleeps for 1 second, then interrupts t1
                Thread.sleep(1000);
                t1.interrupt(); // Interrupt t1

                t1.join(); // Wait for t1 to finish (after interruption)
                System.out.println("Main thread finished.");
            }
        }
        ```

8.  **`yield()`**:
    *   **Purpose**: A **"hint" to the OS scheduler** that the current thread is willing to temporarily yield its current use of a processor. The scheduler is free to ignore this hint. It might allow other threads of the same or higher priority to run. Used to promote better cooperation between threads.
    *   **Example**:
        ```java
        class YieldThread extends Thread {
            public YieldThread(String name) {
                super(name);
            }

            @Override
            public void run() {
                for (int i = 0; i < 5; i++) {
                    System.out.println(getName() + " is running. Iteration: " + i);
                    Thread.yield(); // Hint to scheduler to let other threads run
                }
            }
        }

        public class YieldExample {
            public static void main(String[] args) {
                YieldThread t1 = new YieldThread("Thread-1");
                YieldThread t2 = new YieldThread("Thread-2");

                t1.start();
                t2.start();

                // With yield, output typically shows more interleaving
                // Without yield, one thread might complete more iterations consecutively before the other gets a chance.
            }
        }
        ```

9.  **`setDaemon(boolean on)` / `isDaemon()`**:
    *   **Purpose**: Marks a thread as a **daemon thread** or a user thread.
    *   **User Threads**: These are the default threads created. The **JVM will wait for all user threads to complete their execution** before terminating the program. They perform "useful work" or "business logic".
    *   **Daemon Threads**: These are **background threads**. The **JVM will NOT wait for daemon threads to complete**. If all user threads finish, the JVM terminates, even if daemon threads are still running. Examples in Java include the Garbage Collector. Daemon threads are typically used for supporting tasks that don't need to prevent the application from exiting.
    *   **Example**:
        ```java
        class MyTaskThread extends Thread {
            public MyTaskThread(String name) {
                super(name);
            }

            @Override
            public void run() {
                int count = 0;
                while (true) { // Infinite loop to demonstrate daemon behavior
                    try {
                        System.out.println(getName() + ": Hello World " + count++);
                        Thread.sleep(100);
                    } catch (InterruptedException e) {
                        System.out.println(getName() + " was interrupted.");
                        break;
                    }
                }
                System.out.println(getName() + " terminated."); // This line might not be reached for daemon threads
            }
        }

        public class DaemonThreadExample {
            public static void main(String[] args) throws InterruptedException {
                MyTaskThread userThread = new MyTaskThread("UserThread");
                MyTaskThread daemonThread = new MyTaskThread("DaemonThread");

                // Mark daemonThread as a daemon thread
                daemonThread.setDaemon(true);

                userThread.start();
                daemonThread.start();

                // Main thread finishes quickly
                System.out.println("Main thread finished."); // This will print almost immediately

                // UserThread will continue printing "Hello World"
                // DaemonThread will also continue printing "Hello World"

                // After a short delay, we stop the user thread.
                // Once userThread terminates, the JVM will exit, even if daemonThread is still running.
                Thread.sleep(1000); // Let them run for a bit
                userThread.interrupt(); // Interrupt the user thread to allow JVM to exit
            }
        }
        ```

---

### Synchronization

Synchronization is a mechanism to control access to shared resources by multiple threads, preventing data corruption and ensuring correct results.

*   **The Problem (Race Condition)**: When multiple threads access and modify a **"shared resource"** (like a `count` variable in a `Counter` class) concurrently without proper control, the final result can be **"incorrect" or "unpredictable"**. This situation is known as a **"Race Condition"**. The outcome depends on the relative timing of thread execution.
    *   **Example Scenario**: Two threads simultaneously read a `count` of 100, both increment it, and write back 101. The count should be 102, but ends up as 101 because both operations "raced" and one's update overwrote the other's, or an increment operation might involve multiple CPU instructions (read, increment, write) that can be interleaved by the OS scheduler.

*   **Critical Section**: The part of your program where shared resources are accessed or modified is called the **"Critical Section"**. This section needs to be protected to avoid race conditions.

*   **Solution (`synchronized` keyword)**: The `synchronized` keyword in Java is used to ensure that **only one thread can execute a critical section at a time**. This concept is called **"Mutual Exclusion"**.
    *   **Mutual Exclusion**: Ensures that multiple threads cannot simultaneously access the critical section. It prevents the chaotic interleaving of operations on shared data.
    *   **How `synchronized` works**: When a thread enters a `synchronized` method or block, it acquires an **"intrinsic lock"** (also called a monitor lock) on the object (or class, for static methods). No other thread can acquire that same lock until the current thread releases it (by exiting the `synchronized` block/method).
    *   **`synchronized` Method**:
        ```java
        class Counter {
            private int count = 0;

            // Synchronized method
            public synchronized void increment() { // Acquires lock on 'this' (Counter instance)
                count++;
            }

            public int getCount() {
                return count;
            }
        }
        ```
    *   **`synchronized` Block**: You can synchronize a specific block of code within a method by providing an object to lock on.
        ```java
        class Counter {
            private int count = 0;
            private final Object lock = new Object(); // Object to lock on

            public void increment() {
                // Synchronized block
                synchronized (lock) { // Acquires lock on the 'lock' object
                    count++;
                }
            }

            public int getCount() {
                return count;
            }
        }
        ```
        *Self-correction:* The source primarily uses `synchronized(this)` for block examples and `synchronized` keyword for method. I'll use `this` or a dedicated lock object as mentioned in source.

    *   **Code Example (Race Condition & `synchronized` Solution):**
        ```java
        // Counter.java (as defined above, with synchronized increment method)
        class Counter {
            private int count = 0;

            public synchronized void increment() { // Synchronized method
                // Simulate some work or processing
                // int temp = count;
                // temp = temp + 1;
                // count = temp;
                count++;
            }

            public int getCount() {
                return count;
            }
        }

        class MyThread extends Thread {
            private Counter counter; // Shared Counter object

            public MyThread(Counter counter, String name) {
                super(name);
                this.counter = counter;
            }

            @Override
            public void run() {
                for (int i = 0; i < 1000; i++) { // Increment count 1000 times
                    counter.increment();
                }
            }
        }

        public class SynchronizationExample {
            public static void main(String[] args) throws InterruptedException {
                Counter sharedCounter = new Counter(); // Single shared object

                MyThread t1 = new MyThread(sharedCounter, "Thread-1");
                MyThread t2 = new MyThread(sharedCounter, "Thread-2");

                t1.start();
                t2.start();

                t1.join(); // Wait for t1 to finish
                t2.join(); // Wait for t2 to finish

                // Expected result: 2000 (1000 from t1 + 1000 from t2)
                System.out.println("Finally, Counter Count: " + sharedCounter.getCount());
                // If `increment()` was not synchronized, the result would often be less than 2000 due to race condition.
                // With `synchronized`, it should consistently be 2000.
            }
        }
        ```

---

### Explicit Locks (`java.util.concurrent.locks.Lock`)

While `synchronized` is built-in, explicit locks offer more control and flexibility.

*   **Intrinsic vs. Explicit Locks**:
    *   **Intrinsic Locks (Implicit)**: Used automatically by the `synchronized` keyword. Every Java object inherently has one.
    *   **Explicit Locks (Manual)**: More advanced, allowing developers to control *when* to lock and unlock. They are implemented using the `java.util.concurrent.locks.Lock` interface, with `ReentrantLock` being a common implementation.

*   **Advantages of Explicit Locks over `synchronized`**:
    *   **More Control**: You can decide exactly when to acquire and release the lock.
    *   **Non-blocking Lock Acquisition (`tryLock()`)**: A thread can attempt to acquire a lock without blocking indefinitely if the lock is not available.
    *   **Timed Lock Acquisition (`tryLock(long timeout, TimeUnit unit)`)**: A thread can attempt to acquire a lock and wait for a specified duration. If the lock isn't acquired within that time, it returns `false`.
    *   **Interruptible Lock Acquisition (`lockInterruptibly()`)**: A thread waiting for a lock can be interrupted. `synchronized` locks are not interruptible.
    *   **Fairness**: `ReentrantLock` can be configured for fairness (first-in, first-out access). `synchronized` does not guarantee fairness.
    *   **Read-Write Locking**: Specific locks like `ReentrantReadWriteLock` (discussed later) allow different locking behaviors for read and write operations, something `synchronized` cannot do.

*   **`ReentrantLock`**: An implementation of the `Lock` interface.
    *   **Reentrancy**: A `ReentrantLock` allows the same thread to acquire the same lock multiple times without causing a deadlock. It maintains an internal count of how many times the lock has been acquired by the current thread. The lock is only fully released when the acquisition count returns to zero. This is like having the main key to your house; you can enter any room (acquire inner locks) because you already hold the main key.

*   **Key `Lock` Methods**:
    *   **`lock()`**: Acquires the lock. If the lock is not available, the current thread will wait indefinitely until it acquires the lock. Similar to `synchronized` in its blocking behavior.
    *   **`unlock()`**: Releases the lock. It's crucial to call `unlock()` in a `finally` block to ensure the lock is always released, even if exceptions occur.
    *   **`tryLock()`**: Attempts to acquire the lock. If the lock is available, it acquires it and returns `true`. If not, it returns `false` immediately without waiting.
    *   **`tryLock(long timeout, TimeUnit unit)`**: Attempts to acquire the lock, waiting for a specified `timeout`. Returns `true` if the lock is acquired within the time, `false` otherwise. Can throw `InterruptedException` if the thread is interrupted while waiting.
    *   **`lockInterruptibly()`**: Acquires the lock unless the current thread is interrupted. Throws `InterruptedException` if interrupted.

*   **Code Example (Bank Account with `ReentrantLock`):**
    ```java
    import java.util.concurrent.TimeUnit;
    import java.util.concurrent.locks.Lock;
    import java.util.concurrent.locks.ReentrantLock;

    class BankAccount {
        private int balance = 100; // Shared resource
        private final Lock lock = new ReentrantLock(); // Explicit Lock

        public void withdraw(int amount) {
            String threadName = Thread.currentThread().getName();
            System.out.println(threadName + ": Attempting to withdraw " + amount);

            try {
                // Try to acquire the lock, wait for 1 second
                if (lock.tryLock(1, TimeUnit.SECONDS)) { // Using tryLock with timeout
                    try {
                        if (balance >= amount) { // Critical section check
                            System.out.println(threadName + ": Proceeding with withdrawal.");
                            Thread.sleep(3000); // Simulate processing time (e.g., database transaction)
                            balance -= amount;
                            System.out.println(threadName + ": Completed withdrawal. Remaining Balance: " + balance);
                        } else {
                            System.out.println(threadName + ": Insufficient Balance.");
                        }
                    } catch (InterruptedException e) {
                        System.out.println(threadName + ": Interrupted during withdrawal process.");
                        Thread.currentThread().interrupt(); // Restore interrupt status
                    } finally {
                        lock.unlock(); // Always unlock in finally
                    }
                } else {
                    System.out.println(threadName + ": Could not acquire the lock. Will try again later.");
                    // This thread can now do other work or terminate, instead of waiting indefinitely
                }
            } catch (InterruptedException e) {
                System.out.println(threadName + ": Interrupted while trying to acquire lock.");
                Thread.currentThread().interrupt(); // Restore interrupt status
            }
        }

        public int getBalance() {
            return balance;
        }
    }

    public class ExplicitLockingExample {
        public static void main(String[] args) throws InterruptedException {
            BankAccount account = new BankAccount(); // Shared bank account

            Runnable task = () -> account.withdraw(50); // Task to withdraw 50

            Thread t1 = new Thread(task, "Thread-1");
            Thread t2 = new Thread(task, "Thread-2");

            t1.start();
            t2.start();

            t1.join();
            t2.join();

            System.out.println("Final Account Balance: " + account.getBalance());
        }
    }
    ```
    *   **Explanation**: In this example, `t1` attempts to withdraw first. It acquires the lock and enters a 3-second sleep. `t2` attempts to withdraw almost simultaneously but finds the lock unavailable. Since `tryLock` with a 1-second timeout is used, `t2` waits for 1 second, fails to acquire the lock (because `t1` holds it for 3 seconds), prints "Could not acquire the lock," and exits without blocking indefinitely. `t1` completes its withdrawal, leaving the balance at 50. `t2` doesn't get to withdraw. This demonstrates how `tryLock` avoids indefinite waiting.

---

### Fairness and Starvation

*   **Fairness**: In multithreading, fairness refers to the **order in which waiting threads acquire a lock**. A fair lock ensures that threads acquire the lock in the order they requested it (First-In, First-Out or FIFO). `ReentrantLock` can be constructed with a `true` boolean argument for fairness.
*   **Starvation**: Occurs when a **low-priority thread or a thread that repeatedly loses the race for a resource never gets a chance to run or acquire a necessary resource**. Fair locks can help mitigate starvation by ensuring every waiting thread gets its turn.
    *   **Example (Setting Fairness in `ReentrantLock`):**
        ```java
        // In BankAccount class or any class using ReentrantLock:
        private final Lock lock = new ReentrantLock(true); // 'true' for fair lock
        ```
        *   **Effect**: When `true` is passed, waiting threads will acquire the lock in the order they called `lock()` or `tryLock()`. Without `true` (default is unfair), there's no guaranteed order, and a thread might acquire the lock even if others have been waiting longer.

---

### ReadWriteLock (`java.util.concurrent.locks.ReadWriteLock`)

`synchronized` treats all operations as exclusive, even if multiple threads only want to *read* shared data. `ReadWriteLock` provides a more granular approach.

*   **Purpose**: Allows **multiple threads to read a resource concurrently** while ensuring **exclusive access for write operations**.
*   **Components**: A `ReadWriteLock` object typically provides two `Lock` instances:
    *   **Read Lock (`readLock().lock()`/`readLock().unlock()`)**: Can be acquired by multiple reader threads simultaneously, *as long as no thread holds the write lock*.
    *   **Write Lock (`writeLock().lock()`/`writeLock().unlock()`)**: Can be acquired by only one writer thread at a time. When a write lock is held, no other threads (readers or writers) can acquire any lock.
*   **Implementation**: `ReentrantReadWriteLock` is the common implementation.
*   **Advantage**: Prevents unnecessary blocking for read operations, improving concurrency for read-heavy applications.
*   **Code Example (ReadWriteLock):**
    ```java
    import java.util.concurrent.locks.ReadWriteLock;
    import java.util.concurrent.locks.ReentrantReadWriteLock;
    import java.util.concurrent.locks.Lock;

    class ReadWriteCounter {
        private int count = 0;
        private final ReadWriteLock rwLock = new ReentrantReadWriteLock(); // ReadWriteLock instance
        private final Lock readLock = rwLock.readLock(); // Read lock
        private final Lock writeLock = rwLock.writeLock(); // Write lock

        // Method for reading the count
        public int getCount() {
            readLock.lock(); // Acquire read lock
            try {
                System.out.println(Thread.currentThread().getName() + " acquired Read Lock. Reading count: " + count);
                Thread.sleep(50); // Simulate read time
                return count;
            } catch (InterruptedException e) {
                Thread.currentThread().interrupt();
                return -1;
            } finally {
                readLock.unlock(); // Release read lock
                System.out.println(Thread.currentThread().getName() + " released Read Lock.");
            }
        }

        // Method for incrementing the count
        public void increment() {
            writeLock.lock(); // Acquire write lock
            try {
                System.out.println(Thread.currentThread().getName() + " acquired Write Lock. Incrementing count...");
                Thread.sleep(100); // Simulate write time
                count++;
                System.out.println(Thread.currentThread().getName() + " finished Incrementing. Count: " + count);
            } catch (InterruptedException e) {
                Thread.currentThread().interrupt();
            } finally {
                writeLock.unlock(); // Release write lock
                System.out.println(Thread.currentThread().getName() + " released Write Lock.");
            }
        }
    }

    public class ReadWriteLockExample {
        public static void main(String[] args) throws InterruptedException {
            ReadWriteCounter counter = new ReadWriteCounter(); // Shared counter

            Runnable readerTask = () -> {
                for (int i = 0; i < 5; i++) {
                    counter.getCount(); // Read the count
                }
            };

            Runnable writerTask = () -> {
                for (int i = 0; i < 2; i++) {
                    counter.increment(); // Increment the count
                }
            };

            Thread writerThread = new Thread(writerTask, "WriterThread");
            Thread readerThread1 = new Thread(readerTask, "ReaderThread-1");
            Thread readerThread2 = new Thread(readerTask, "ReaderThread-2");

            writerThread.start();
            // Introduce a small delay to allow writer to acquire lock first
            Thread.sleep(10);
            readerThread1.start();
            readerThread2.start();

            writerThread.join();
            readerThread1.join();
            readerThread2.join();

            System.out.println("Final Count: " + counter.count);
        }
    }
    ```
    *   **Explanation**: When the `WriterThread` holds the `writeLock`, both `ReaderThread-1` and `ReaderThread-2` will block. However, once the `writeLock` is released, both reader threads can acquire the `readLock` *simultaneously* and perform their read operations in parallel. This demonstrates how `ReadWriteLock` allows higher concurrency for read operations.

---

### Deadlock

Deadlock is a critical issue in concurrent programming where threads get stuck waiting for each other indefinitely.

*   **Definition**: A situation in multithreading where two or more threads are **permanently blocked, waiting for each other** to release a resource that the other thread holds.
*   **Conditions for Deadlock (Necessary Conditions)**: For a deadlock to occur, all four of these conditions must typically be met:
    1.  **Mutual Exclusion**: Resources involved must be non-shareable, meaning only one thread can use them at a time (e.g., critical sections protected by locks).
    2.  **Hold and Wait**: A thread must be holding at least one resource while waiting to acquire another resource held by another thread.
    3.  **No Preemption**: Resources cannot be forcibly taken from a thread; they must be voluntarily released.
    4.  **Circular Wait**: A circular chain of threads exists, where each thread in the chain is waiting for a resource held by the next thread in the chain.
*   **Real-life Analogy**: Person A has a pen and needs paper from Person B. Person B has paper and needs a pen from Person A. Both are waiting indefinitely, leading to no work being done.

*   **Code Example (Deadlock Scenario - Pen and Paper):**
    ```java
    // Pen.java
    class Pen {
        public synchronized void writeWithPenAndPaper(Paper paper) { // Holds lock on Pen
            System.out.println(Thread.currentThread().getName() + " is using Pen and is trying to use Paper.");
            // Trying to acquire lock on Paper
            paper.finishWriting(); // Calls synchronized method on Paper, requiring Paper's lock
        }

        public synchronized void finishWriting() {
            System.out.println(Thread.currentThread().getName() + " finished writing with Pen.");
        }
    }

    // Paper.java
    class Paper {
        public synchronized void writeWithPaperAndPen(Pen pen) { // Holds lock on Paper
            System.out.println(Thread.currentThread().getName() + " is using Paper and is trying to use Pen.");
            // Trying to acquire lock on Pen
            pen.finishWriting(); // Calls synchronized method on Pen, requiring Pen's lock
        }

        public synchronized void finishWriting() {
            System.out.println(Thread.currentThread().getName() + " finished writing with Paper.");
        }
    }

    // DeadlockExample.java
    public class DeadlockExample {
        public static void main(String[] args) {
            Pen pen = new Pen();
            Paper paper = new Paper();

            // Task 1: Tries to get Pen, then Paper
            Thread task1 = new Thread(() -> {
                pen.writeWithPenAndPaper(paper);
            }, "Thread-1");

            // Task 2: Tries to get Paper, then Pen
            Thread task2 = new Thread(() -> {
                paper.writeWithPaperAndPen(pen);
            }, "Thread-2");

            task1.start();
            task2.start();
            // This program will likely hang due to deadlock.
        }
    }
    ```
    *   **Explanation**:
        *   `Thread-1` calls `pen.writeWithPenAndPaper(paper)`. It acquires the lock on `pen`. Inside, it tries to call `paper.finishWriting()`, which requires the lock on `paper`.
        *   Simultaneously, `Thread-2` calls `paper.writeWithPaperAndPen(pen)`. It acquires the lock on `paper`. Inside, it tries to call `pen.finishWriting()`, which requires the lock on `pen`.
        *   `Thread-1` holds `pen` and waits for `paper`. `Thread-2` holds `paper` and waits for `pen`. A circular dependency forms, leading to deadlock.

*   **Resolving Deadlock (Consistent Lock Ordering)**:
    *   **Strategy**: The most common approach is to **ensure that all threads acquire locks in a consistent, predefined order**.
    *   **Solution for Pen and Paper Example**: Both threads should try to acquire the `Pen` lock first, then the `Paper` lock.
    ```java
    // ... (Pen.java and Paper.java remain the same) ...

    public class DeadlockResolutionExample {
        public static void main(String[] args) {
            Pen pen = new Pen();
            Paper paper = new Paper();

            // Task 1: Acquires Pen lock, then Paper lock
            Thread task1 = new Thread(() -> {
                synchronized (pen) { // Acquire pen lock first
                    System.out.println(Thread.currentThread().getName() + " acquired Pen. Trying to get Paper.");
                    synchronized (paper) { // Then acquire paper lock
                        System.out.println(Thread.currentThread().getName() + " acquired Paper. Writing...");
                        // Actual work
                        System.out.println(Thread.currentThread().getName() + " finished writing.");
                    }
                }
            }, "Thread-1");

            // Task 2: Also acquires Pen lock, then Paper lock (consistent order)
            Thread task2 = new Thread(() -> {
                synchronized (pen) { // Acquire pen lock first
                    System.out.println(Thread.currentThread().getName() + " acquired Pen. Trying to get Paper.");
                    synchronized (paper) { // Then acquire paper lock
                        System.out.println(Thread.currentThread().getName() + " acquired Paper. Writing...");
                        // Actual work
                        System.out.println(Thread.currentThread().getName() + " finished writing.");
                    }
                }
            }, "Thread-2");

            task1.start();
            task2.start();
            // This program will now execute successfully without deadlock.
        }
    }
    ```
    *   **Explanation**: Now, both `Thread-1` and `Thread-2` try to acquire the `pen` lock first. Only one of them will succeed. The successful thread will then proceed to acquire the `paper` lock. Once it finishes its work and releases both locks, the other thread can acquire them in the same order.

---

### Thread Communication

In a multithreading environment, threads often need to communicate and coordinate their activities.

*   **Problem without Communication (Busy Waiting)**: Without proper thread communication, threads might fall into a "busy waiting" state. This means they continuously check a condition (e.g., "Is data available?") using CPU resources, which leads to **wastage of CPU resources** and potential deadlocks.
    *   **Example**: A consumer thread constantly checking if a producer thread has put data into a buffer.

*   **Solution (`wait()`, `notify()`, `notifyAll()`)**: Java's `Object` class provides these methods for inter-thread communication.
    *   **Important Note**: These methods **can only be called within a `synchronized` context** (method or block). When `wait()` is called, the current thread releases the lock it holds.
    *   **`wait()`**: Causes the **current thread to release the lock** on the object and **wait indefinitely** until another thread calls `notify()` or `notifyAll()` on the *same object*. It can throw `InterruptedException`.
    *   **`notify()`**: Wakes up a **single thread** that is waiting on the object's lock. If multiple threads are waiting, it's non-deterministic which one gets woken up.
    *   **`notifyAll()`**: Wakes up **all threads** that are waiting on the object's lock.

*   **Code Example (Producer-Consumer with `wait()` and `notify()`):**
    ```java
    class SharedResource {
        private String data; // Shared data
        private boolean hasData = false; // Flag to indicate data availability

        // Producer method
        public synchronized void produce(String value) { // Synchronized context
            while (hasData) { // If data exists, producer must wait
                try {
                    System.out.println(Thread.currentThread().getName() + ": Data exists, Producer waiting...");
                    wait(); // Release lock and wait
                } catch (InterruptedException e) {
                    Thread.currentThread().interrupt();
                    return;
                }
            }
            this.data = value; // Produce data
            this.hasData = true; // Set flag to true
            System.out.println(Thread.currentThread().getName() + ": Produced: " + data);
            notify(); // Notify waiting consumer
        }

        // Consumer method
        public synchronized String consume() { // Synchronized context
            while (!hasData) { // If no data, consumer must wait
                try {
                    System.out.println(Thread.currentThread().getName() + ": No data, Consumer waiting...");
                    wait(); // Release lock and wait
                } catch (InterruptedException e) {
                    Thread.currentThread().interrupt();
                    return null;
                }
            }
            String consumedData = this.data; // Consume data
            this.hasData = false; // Set flag to false
            System.out.println(Thread.currentThread().getName() + ": Consumed: " + consumedData);
            notify(); // Notify waiting producer
            return consumedData;
        }
    }

    class Producer extends Thread {
        private SharedResource resource;

        public Producer(SharedResource resource, String name) {
            super(name);
            this.resource = resource;
        }

        @Override
        public void run() {
            for (int i = 0; i < 5; i++) {
                resource.produce("Data-" + i); // Produce data
                try {
                    Thread.sleep(500); // Simulate some work
                } catch (InterruptedException e) {
                    Thread.currentThread().interrupt();
                }
            }
        }
    }

    class Consumer extends Thread {
        private SharedResource resource;

        public Consumer(SharedResource resource, String name) {
            super(name);
            this.resource = resource;
        }

        @Override
        public void run() {
            for (int i = 0; i < 5; i++) {
                resource.consume(); // Consume data
                try {
                    Thread.sleep(1000); // Simulate some work
                } catch (InterruptedException e) {
                    Thread.currentThread().interrupt();
                }
            }
        }
    }

    public class ThreadCommunicationExample {
        public static void main(String[] args) throws InterruptedException {
            SharedResource resource = new SharedResource();

            Producer producer = new Producer(resource, "ProducerThread");
            Consumer consumer = new Consumer(resource, "ConsumerThread");

            producer.start();
            consumer.start();

            producer.join();
            consumer.join();

            System.out.println("Producer and Consumer finished.");
        }
    }
    ```
    *   **Explanation**: The `while` loops with `wait()` ensure that `produce` waits if data is present and `consume` waits if no data is present, preventing busy waiting. `notify()` (or `notifyAll()` if multiple consumers/producers) wakes up the waiting thread to continue its work. This ensures efficient use of CPU resources.

---

### Thread Safety

Thread safety is a property of code or an object that ensures correct behavior when accessed by multiple threads concurrently.

*   **Definition**: An object or a block of code is considered **"thread-safe"** if it **guarantees "unexpected results" or "race conditions" will not occur** when multiple threads attempt to access it simultaneously. It ensures data integrity and correctness.
*   **Achieving Thread Safety**: All the mechanisms discussed so far (synchronization, explicit locks, thread communication) are primarily aimed at **achieving thread safety**.
*   **Examples (Not thread-safe vs. Thread-safe - discussed in source but not detailed code)**: The source mentions `StringBuilder` vs. `StringBuffer` vs. `String` as future examples where `StringBuffer` is thread-safe and `StringBuilder` is not. This distinction would further clarify the concept.

---

### Lambda Expressions in Java 8+

Lambda expressions provide a concise way to represent anonymous functions. They are particularly useful for working with functional interfaces.

*   **Anonymous Function**: A lambda expression is essentially an anonymous function – a function without a name.
*   **Functional Interface**: A functional interface is any interface that **contains exactly one abstract method**. They can have any number of default or static methods. `Runnable` and `Callable` are examples of functional interfaces.
*   **Syntax**: The basic syntax is `(parameters) -> { body }`.
    *   If there's only one parameter, parentheses can be omitted: `parameter -> { body }`.
    *   If the body contains a single expression, curly braces and the `return` keyword (if applicable) can be omitted: `(parameters) -> expression`.

*   **Simplifying Thread Creation**: Lambda expressions simplify creating instances of functional interfaces, like `Runnable`, making thread creation more concise.

*   **Code Example (Thread Creation with Lambda):**
    ```java
    public class LambdaThreadExample {
        public static void main(String[] args) {
            // Traditional Anonymous Inner Class for Runnable
            Runnable runnableOldWay = new Runnable() {
                @Override
                public void run() {
                    System.out.println(Thread.currentThread().getName() + ": Hello from old Runnable.");
                }
            };
            Thread t1 = new Thread(runnableOldWay);
            t1.start();

            // Using Lambda Expression for Runnable
            Runnable runnableLambda = () -> { // Parameters are empty for run() method
                for (int i = 0; i < 5; i++) {
                    System.out.println(Thread.currentThread().getName() + ": Hello from Lambda. Iteration: " + i);
                }
            };
            Thread t2 = new Thread(runnableLambda, "LambdaThread-1");
            t2.start();

            // Even more concise, directly in Thread constructor
            Thread t3 = new Thread(() -> { // Direct lambda for Runnable
                System.out.println(Thread.currentThread().getName() + ": Hello from concise Lambda.");
            }, "LambdaThread-2");
            t3.start();

            // With multiple lines in lambda body
            Thread t4 = new Thread(() -> {
                for (int i = 0; i < 3; i++) {
                    System.out.println(Thread.currentThread().getName() + ": Multi-line Lambda: " + i);
                }
            }, "LambdaThread-3");
            t4.start();

            // Lambda for a custom functional interface (example for illustration from source)
            // Suppose Student is a functional interface:
            // interface Student { String getBio(String name); }
            // Student engineeringStudent = (name) -> name + " is Engineering Student";
            // System.out.println(engineeringStudent.getBio("Ram"));
        }
    }
    ```

---

### Thread Pools and Executor Framework

Manually creating and managing threads for every task is inefficient and prone to errors. The Executor Framework provides a structured way to manage threads using "thread pools".

*   **Problem with Manual Thread Management**:
    *   **Resource Overhead**: Creating and destroying a new thread for every task is computationally expensive and has an "overhead".
    *   **Poor Resource Management**: Can lead to inefficient use of system resources and unpredictable performance.
    *   **Scalability Issues**: If a large number of tasks arrive simultaneously, creating too many threads can overload the system.
    *   **Complexity**: Manual error handling and thread lifecycle management become complex.

*   **Thread Pools**: A **"collection of pre-initialized threads"** that are ready to perform tasks. Instead of creating a new thread for each task, tasks are submitted to the pool, and an available thread from the pool executes them.
    *   **Benefits of Thread Pools**:
        *   **Resource Management**: Reduces the overhead of thread creation/destruction. Threads are reused.
        *   **Improved Responsiveness**: Tasks can start execution faster as threads are already created.
        *   **Controlled Thread Count**: Limits the maximum number of active threads, preventing system overload.
        *   **Simplified Management**: Abstracts away the complexities of low-level thread management.

*   **Executor Framework (Java 5+)**: A set of interfaces and classes in `java.util.concurrent` that simplify concurrent application development.
    *   **Core Interfaces**:
        1.  **`Executor`**: The simplest interface. It defines a single method, `execute(Runnable command)`, which executes the given command. It does not provide shutdown mechanisms or ways to retrieve results.
        2.  **`ExecutorService`**: Extends `Executor` and provides methods for managing the lifecycle of the executor (e.g., `shutdown()`, `shutdownNow()`) and for submitting tasks that can return results (e.g., `submit(Callable<T> task)`, `invokeAll()`, `invokeAny()`).
        3.  **`ScheduledExecutorService`**: Extends `ExecutorService` and adds methods for scheduling tasks to run after a delay or periodically.

*   **`Executors` Utility Class**: Provides factory methods to create various types of `ExecutorService` instances.
    *   **`Executors.newFixedThreadPool(int nThreads)`**: Creates a thread pool with a **fixed number of threads**. If more tasks are submitted than available threads, tasks wait in a queue.
    *   **`Executors.newSingleThreadExecutor()`**: Creates an `ExecutorService` that uses a **single worker thread**. All tasks are executed sequentially in this one thread.
    *   **`Executors.newCachedThreadPool()`**: Creates a thread pool that **creates new threads as needed** but reuses existing idle threads. If a thread is idle for 60 seconds, it is terminated. This pool is suitable for applications with a variable and often short-lived task load. **Risk**: Can create too many threads if tasks are long-lived and variable, potentially exhausting system resources.

*   **Submitting Tasks**:
    *   **`execute(Runnable command)` (from `Executor`)**: Executes the given `Runnable` task. Does not return a result.
    *   **`submit(Runnable task)` (from `ExecutorService`)**: Submits a `Runnable` task for execution. Returns a `Future<?>` object. The `Future` object can be used to check the task's status (e.g., `isDone()`) but `get()` will return `null` as `Runnable` doesn't return a value.
    *   **`submit(Callable<T> task)` (from `ExecutorService`)**: Submits a `Callable` task for execution. `Callable` is a functional interface with a `call()` method that can **return a result** (`T`) and **throw an exception**. Returns a `Future<T>` object, from which the result can be retrieved using `get()`.

*   **`Future<T>` Interface**: Represents the **result of an asynchronous computation**.
    *   **`get()`**: **Blocks** the current thread until the computation is complete, and then retrieves its result. Can throw `InterruptedException` or `ExecutionException`.
    *   **`get(long timeout, TimeUnit unit)`**: Blocks for a specified time to get the result. Throws `TimeoutException` if the result is not available within the timeout.
    *   **`isDone()`**: Returns `true` if the task has completed (normally, via exception, or cancelled), `false` otherwise.
    *   **`isCancelled()`**: Returns `true` if the task was cancelled before it completed normally.
    *   **`cancel(boolean mayInterruptIfRunning)`**: Attempts to cancel the execution of this task. `mayInterruptIfRunning=true` attempts to interrupt the task if it's currently running. If `false`, a running task is not interrupted.

*   **Managing ExecutorService Lifecycle**:
    *   **`shutdown()`**: Initiates an **orderly shutdown**. It stops accepting new tasks but waits for all previously submitted tasks to complete before terminating the pool.
    *   **`shutdownNow()`**: Attempts to stop all actively executing tasks, halts the processing of waiting tasks, and returns a list of the tasks that were awaiting execution. It does not wait for active tasks to complete.
    *   **`awaitTermination(long timeout, TimeUnit unit)`**: Blocks until all tasks have completed execution after a `shutdown()` request, or the timeout occurs, or the current thread is interrupted. Returns `true` if terminated, `false` if the timeout elapsed before termination.
    *   **`isShutdown()`**: Returns `true` if `shutdown()` has been called.
    *   **`isTerminated()`**: Returns `true` if all tasks have completed following a shutdown request.

*   **Code Example (Factorial Calculation with `ExecutorService`):**
    ```java
    import java.util.concurrent.*;
    import java.util.ArrayList;
    import java.util.List;

    public class ExecutorServiceFactorialExample {

        // Dummy factorial method that simulates heavy computation
        private static long factorial(int n) {
            if (n < 0) throw new IllegalArgumentException("Factorial not defined for negative numbers");
            if (n == 0 || n == 1) return 1;
            long result = 1;
            for (int i = 2; i <= n; i++) {
                result *= i;
            }
            try {
                Thread.sleep(100); // Simulate 100ms computation time
            } catch (InterruptedException e) {
                Thread.currentThread().interrupt();
            }
            return result;
        }

        public static void main(String[] args) throws InterruptedException, ExecutionException {
            // Using a FixedThreadPool with 3 threads
            ExecutorService executor = Executors.newFixedThreadPool(3); // 3 worker threads

            long startTime = System.currentTimeMillis();

            List<Future<Long>> futures = new ArrayList<>();

            for (int i = 1; i <= 9; i++) { // Calculate factorial for numbers 1 to 9
                final int num = i; // Must be final or effectively final for lambda
                // Submit tasks as Callable (since we want a result)
                futures.add(executor.submit(() -> { // Lambda for Callable
                    long result = factorial(num);
                    System.out.println(Thread.currentThread().getName() + ": Factorial of " + num + " is " + result);
                    return result;
                }));
            }

            // Wait for all tasks to complete and retrieve results
            for (Future<Long> future : futures) {
                future.get(); // Blocks until task completes
            }

            executor.shutdown(); // Initiate orderly shutdown
            // Wait for all tasks to terminate
            executor.awaitTermination(60, TimeUnit.SECONDS); // Max wait of 60 seconds

            long endTime = System.currentTimeMillis();
            System.out.println("Total time taken: " + (endTime - startTime) + " ms");
            // Expected: significantly faster than sequential execution (e.g., ~1 second for 9 tasks with 3 threads if ideal)
        }
    }
    ```
    *   **Explanation**: This example efficiently calculates factorials using a thread pool. Instead of creating 9 new threads, 3 threads from the pool are reused. `submit()` is used with `Callable` to get the factorial result, and `future.get()` is used to wait for each individual task's completion, ensuring the total time measurement is accurate.

---

### ScheduledExecutorService

`ScheduledExecutorService` is used for scheduling tasks to run after a specific delay or at regular intervals.

*   **Creation**: `Executors.newScheduledThreadPool(int corePoolSize)`.
*   **Key Scheduling Methods**:
    *   **`schedule(Runnable command, long delay, TimeUnit unit)`**: Schedules a `Runnable` task to be executed after a `delay`. Returns a `ScheduledFuture<?>`.
    *   **`schedule(Callable<V> callable, long delay, TimeUnit unit)`**: Schedules a `Callable` task to be executed after a `delay`. Returns a `ScheduledFuture<V>`.
    *   **`scheduleAtFixedRate(Runnable command, long initialDelay, long period, TimeUnit unit)`**: Schedules a `Runnable` task to execute repeatedly. The `period` is the time *between the start of successive executions*, regardless of how long the task itself takes.
    *   **`scheduleWithFixedDelay(Runnable command, long initialDelay, long delay, TimeUnit unit)`**: Schedules a `Runnable` task to execute repeatedly. The `delay` is the time *between the end of one execution and the start of the next*. This prevents overlapping executions if a task takes longer than its period.

*   **Code Example (Scheduled Tasks):**
    ```java
    import java.util.concurrent.*;

    public class ScheduledExecutorServiceExample {
        public static void main(String[] args) throws InterruptedException {
            // Create a scheduled thread pool with 1 thread
            ScheduledExecutorService scheduler = Executors.newScheduledThreadPool(1);

            // Task 1: Schedule a one-time task after a delay
            System.out.println("Scheduling one-time task in 2 seconds...");
            scheduler.schedule(() -> { // Runnable lambda
                System.out.println("One-time task executed after 2 seconds.");
            }, 2, TimeUnit.SECONDS);

            // Task 2: Schedule a periodic task with fixed rate
            // Initial delay of 1 second, then runs every 3 seconds (start to start)
            System.out.println("Scheduling fixed-rate task (initial 1s, then every 3s)...");
            ScheduledFuture<?> fixedRateFuture = scheduler.scheduleAtFixedRate(() -> {
                System.out.println("Fixed-rate task: " + System.currentTimeMillis() / 1000);
                try {
                    Thread.sleep(1000); // Task takes 1 second to complete
                } catch (InterruptedException e) {
                    Thread.currentThread().interrupt();
                }
            }, 1, 3, TimeUnit.SECONDS); // Initial delay 1s, period 3s

            // Task 3: Schedule a periodic task with fixed delay
            // Initial delay of 1 second, then waits 3 seconds AFTER task finishes
            System.out.println("Scheduling fixed-delay task (initial 1s, then 3s after previous finish)...");
            ScheduledFuture<?> fixedDelayFuture = scheduler.scheduleWithFixedDelay(() -> {
                System.out.println("Fixed-delay task: " + System.currentTimeMillis() / 1000);
                try {
                    Thread.sleep(1000); // Task takes 1 second to complete
                } catch (InterruptedException e) {
                    Thread.currentThread().interrupt();
                }
            }, 1, 3, TimeUnit.SECONDS); // Initial delay 1s, delay 3s


            // Schedule a shutdown task after 10 seconds to stop periodic tasks
            scheduler.schedule(() -> {
                System.out.println("Initiating orderly shutdown...");
                scheduler.shutdown(); // Stop accepting new tasks and finish current ones
                fixedRateFuture.cancel(false); // Can also cancel individual futures if needed
                fixedDelayFuture.cancel(false);
            }, 10, TimeUnit.SECONDS);

            // This main thread does not block, but the scheduler is working in background.
            // Await termination of the scheduler to ensure program exits after tasks complete.
            try {
                if (!scheduler.awaitTermination(20, TimeUnit.SECONDS)) { // Wait up to 20 seconds for termination
                    System.out.println("Scheduler did not terminate within the allotted time. Forcing shutdown...");
                    scheduler.shutdownNow(); // Force shutdown if it doesn't terminate
                }
            } catch (InterruptedException e) {
                System.out.println("Main thread interrupted while waiting for scheduler termination.");
                Thread.currentThread().interrupt();
            }

            System.out.println("Main method finished.");
        }
    }
    ```
    *   **Explanation**: This example shows how to schedule single and periodic tasks. The `scheduleAtFixedRate` will try to run every `period` seconds from the start of the previous execution, even if the task overruns. `scheduleWithFixedDelay` ensures a fixed `delay` *after* the previous task completes, preventing overlaps. A final scheduled task is used to `shutdown` the scheduler after a certain time, preventing indefinite execution of periodic tasks.

---

### CountDownLatch

`CountDownLatch` is a synchronization aid that allows one or more threads to **wait until a set of operations being performed in other threads completes**.

*   **Purpose**: Used when a main thread needs to wait for multiple other threads to finish their work before it proceeds.
*   **How it works**:
    1.  Initialized with a **count** (number of events/threads to wait for) in its constructor.
    2.  The main thread (or any waiting thread) calls `latch.await()`. This blocks the thread until the latch's count reaches zero.
    3.  Each worker thread, upon completing its part of the work, calls `latch.countDown()`. This decrements the latch's count.
    4.  When the count reaches zero, all threads waiting on `await()` are released.
*   **Key Characteristic**: **Not reusable**. Once the count reaches zero, it cannot be reset.

*   **Code Example (Dependent Services with `CountDownLatch`):**
    ```java
    import java.util.concurrent.*;

    class DependentService implements Callable<String> { // Using Callable for simplicity
        private CountDownLatch latch; // Shared CountDownLatch object
        private String serviceName;
        private int delaySeconds;

        public DependentService(CountDownLatch latch, String serviceName, int delaySeconds) {
            this.latch = latch;
            this.serviceName = serviceName;
            this.delaySeconds = delaySeconds;
        }

        @Override
        public String call() { // Changed to call() from run() for Callable
            try {
                System.out.println(serviceName + " started initialization.");
                Thread.sleep(delaySeconds * 1000); // Simulate initialization time
                System.out.println(serviceName + " completed initialization.");
            } catch (InterruptedException e) {
                System.out.println(serviceName + " interrupted during initialization.");
                Thread.currentThread().interrupt();
            } finally {
                latch.countDown(); // Decrement the latch count when done
                System.out.println(serviceName + " counted down. Latch count: " + latch.getCount());
            }
            return serviceName + " initialized.";
        }
    }

    public class CountDownLatchExample {
        public static void main(String[] args) throws InterruptedException, ExecutionException {
            int numberOfServices = 3; // Number of services to wait for
            CountDownLatch startSignal = new CountDownLatch(numberOfServices); // Initialize latch with count

            ExecutorService executor = Executors.newFixedThreadPool(numberOfServices); // Pool for services

            // Submit dependent services as tasks
            executor.submit(new DependentService(startSignal, "Web Server", 2));
            executor.submit(new DependentService(startSignal, "Database", 3));
            executor.submit(new DependentService(startSignal, "Messaging Service", 1));

            System.out.println("Main service waiting for all dependent services to initialize...");
            startSignal.await(); // Main thread waits here until latch count reaches zero
            System.out.println("All dependent services initialized. Starting main service now.");

            executor.shutdown();
            executor.awaitTermination(60, TimeUnit.SECONDS);
        }
    }
    ```
    *   **Explanation**: The `main` method (representing the main service) waits for the `CountDownLatch`. Each `DependentService` task decrements the latch upon completion. Once all three services have `countDown()`ed, the latch's count becomes zero, and the `main` method proceeds. This is ideal for scenarios like application startup where multiple components must initialize before the main application can start.

---

### CyclicBarrier

`CyclicBarrier` is a synchronization aid that enables a **set of threads to wait for each other to reach a common barrier point**.

*   **Purpose**: Used when a group of threads must all reach a certain point before any of them can proceed. It's "cyclic" because it can be reused once the barrier is tripped.
*   **How it works**:
    1.  Initialized with the **number of parties** (threads) that need to arrive at the barrier.
    2.  Each thread, upon reaching the barrier point, calls `barrier.await()`. This blocks the thread.
    3.  When the last thread arrives at the barrier and calls `await()`, all waiting threads are released.
    4.  An optional **"barrier action"** (a `Runnable`) can be provided in the constructor; this action is executed by the last thread once all parties arrive, but *before* any waiting threads are released.
*   **Key Characteristic**: **Reusable**. The barrier can be reset after it has been tripped, allowing the same set of threads to reuse it for subsequent phases of computation.

*   **Real-life Analogy**: A group of friends deciding to watch a movie together: they all agree to wait at the entrance (the barrier) until everyone arrives before entering the theater and starting the movie.

*   **Code Example (Multi-Phase System Startup with `CyclicBarrier`):**
    ```java
    import java.util.concurrent.*;

    class SubsystemInitializer implements Runnable {
        private CyclicBarrier barrier; // Shared CyclicBarrier object
        private String subsystemName;
        private int initializationTime;

        public SubsystemInitializer(CyclicBarrier barrier, String subsystemName, int initializationTime) {
            this.barrier = barrier;
            this.subsystemName = subsystemName;
            this.initializationTime = initializationTime;
        }

        @Override
        public void run() {
            try {
                System.out.println(subsystemName + " starting initialization. Phase 1.");
                Thread.sleep(initializationTime * 1000); // Simulate initialization
                System.out.println(subsystemName + " completed initialization. Waiting at barrier.");

                // Threads wait here for all other subsystems to complete their initialization
                barrier.await(); // Blocks until all parties arrive

                System.out.println(subsystemName + " proceeding to next phase. Phase 2.");
                Thread.sleep(1000); // Simulate second phase work
                System.out.println(subsystemName + " finished Phase 2.");
                barrier.await(); // Can be used for another synchronization point

            } catch (InterruptedException | BrokenBarrierException e) {
                System.out.println(subsystemName + " was interrupted or barrier was broken.");
                Thread.currentThread().interrupt();
            }
        }
    }

    public class CyclicBarrierExample {
        public static void main(String[] args) throws InterruptedException {
            int numberOfSubsystems = 4;

            // Barrier action: executed when all parties reach the barrier
            Runnable barrierAction = () -> System.out.println("\nAll subsystems are UP AND RUNNING! System Startup Complete.\n");

            // Create CyclicBarrier
            CyclicBarrier barrier = new CyclicBarrier(numberOfSubsystems, barrierAction); // With barrier action

            ExecutorService executor = Executors.newFixedThreadPool(numberOfSubsystems);

            executor.submit(new SubsystemInitializer(barrier, "Web Server", 2));
            executor.submit(new SubsystemInitializer(barrier, "Database", 3));
            executor.submit(new SubsystemInitializer(barrier, "Caching Service", 1));
            executor.submit(new SubsystemInitializer(barrier, "Messaging Queue", 4));

            executor.shutdown();
            executor.awaitTermination(30, TimeUnit.SECONDS);

            System.out.println("Main method finished.");
        }
    }
    ```
    *   **Explanation**: In this example, four "subsystems" (Web Server, Database, etc.) initialize. After their initial setup, they all call `barrier.await()`. No subsystem will proceed to "Phase 2" until *all* four have completed "Phase 1" and reached the barrier. Once the last subsystem arrives, the `barrierAction` is executed, and then all subsystems proceed. The barrier can be reused for subsequent phases if needed.

---

### CompletableFuture (Java 8+)

`CompletableFuture` is a powerful tool introduced in Java 8 for **asynchronous programming** and building non-blocking, reactive applications. It represents a `Future` that can be explicitly completed (set its value or exception) and supports chaining dependent actions.

*   **Asynchronous Programming**: A broader term referring to executing tasks without blocking the main thread. `CompletableFuture` facilitates this by allowing tasks to run in a separate thread, and then defining actions to take once the task is complete, without waiting for it.
*   **Core Concepts**:
    *   **`supplyAsync(Supplier<U> supplier)`**: Runs a `Supplier` (a lambda that returns a result) asynchronously. It typically executes in the `ForkJoinPool.commonPool()` but can take a custom `Executor`. Returns a `CompletableFuture<U>`.
    *   **`runAsync(Runnable runnable)`**: Runs a `Runnable` (a lambda that doesn't return a result) asynchronously.
*   **Retrieving Results**:
    *   **`get()`**: Inherited from `Future`, this method **blocks** the calling thread until the `CompletableFuture` completes and returns its result. Throws `InterruptedException` or `ExecutionException`.
    *   **`join()`**: Similar to `get()`, it waits for the result but **does not throw checked exceptions** (it throws `CompletionException` if the computation completes exceptionally). Often preferred in lambda chains.
    *   **`getNow(T valueIfAbsent)`**: Returns the result if available, otherwise returns the `valueIfAbsent` provided. It **does not block**.
*   **Chaining and Composition**: `CompletableFuture` allows chaining of dependent tasks, enabling complex asynchronous workflows.
    *   **`thenApply(Function<? super T,? extends U> fn)`**: Processes the result of the previous `CompletableFuture` with a `Function`.
    *   **`thenAccept(Consumer<? super T> action)`**: Consumes the result of the previous `CompletableFuture` with a `Consumer` (no return value).
    *   **`thenRun(Runnable action)`**: Executes a `Runnable` after the previous `CompletableFuture` completes (does not use its result).
    *   **`allOf(CompletableFuture<?>... cfs)`**: Returns a new `CompletableFuture` that is completed when **all** the given `CompletableFutures` complete. Useful for waiting on multiple independent asynchronous tasks. The returned `CompletableFuture`'s `get()` method will return `null` if all input futures were successful, or throw an exception if any failed.
    *   **`anyOf(CompletableFuture<?>... cfs)`**: Returns a new `CompletableFuture` that is completed when **any** of the given `CompletableFutures` complete (with its result).

*   **Error Handling**:
    *   **`exceptionally(Function<Throwable, ? extends T> fn)`**: Allows you to handle exceptions that occur during the computation.
    *   **`handle(BiFunction<? super T, Throwable, ? extends U> fn)`**: Allows handling both successful results and exceptions.

*   **Timeouts**:
    *   **`orTimeout(long timeout, TimeUnit unit)`**: Completes this `CompletableFuture` with a `TimeoutException` if it is not completed before the given timeout.
    *   **`completeOnTimeout(T value, long timeout, TimeUnit unit)`**: Completes this `CompletableFuture` with the given value if it is not completed before the given timeout.

*   **Code Example (Basic `CompletableFuture` & Chaining):**
    ```java
    import java.util.concurrent.*;
    import java.util.function.Function;

    public class CompletableFutureExample {
        public static void main(String[] args) throws InterruptedException, ExecutionException, TimeoutException {

            // --- 1. Basic supplyAsync and get ---
            System.out.println("--- Basic supplyAsync ---");
            // Run a task asynchronously that returns a String after 2 seconds
            CompletableFuture<String> future1 = CompletableFuture.supplyAsync(() -> {
                try {
                    System.out.println(Thread.currentThread().getName() + ": WorkerThread started."); // Print from worker thread
                    Thread.sleep(2000); // Simulate heavy work
                } catch (InterruptedException e) {
                    Thread.currentThread().interrupt();
                }
                return "Result from Async Task"; // Result
            });

            System.out.println("Main thread continues immediately."); // Main thread is non-blocking

            // Get the result (this will block the main thread)
            String result = future1.get(); // Blocks until future1 completes
            System.out.println("Received result: " + result);


            // --- 2. Using getNow (non-blocking) ---
            System.out.println("\n--- Using getNow ---");
            CompletableFuture<String> future2 = CompletableFuture.supplyAsync(() -> {
                try {
                    Thread.sleep(3000); // Simulate 3 seconds work
                } catch (InterruptedException e) {
                    Thread.currentThread().interrupt();
                }
                return "Actual Result";
            });

            // getNow returns default value if not completed immediately
            String immediateResult = future2.getNow("Default Value if not done");
            System.out.println("Immediate result: " + immediateResult); // Will be "Default Value if not done"

            Thread.sleep(3500); // Wait for future2 to complete
            String finalResult = future2.getNow("Should not be seen");
            System.out.println("Final result after delay: " + finalResult); // Will be "Actual Result"


            // --- 3. Chaining with thenApply ---
            System.out.println("\n--- Chaining with thenApply ---");
            CompletableFuture<String> chainedFuture = CompletableFuture.supplyAsync(() -> "Hello")
                .thenApply(s -> { // Processes the result of previous future
                    System.out.println(Thread.currentThread().getName() + ": Transforming 'Hello'");
                    return s + " World";
                })
                .thenApply(s -> {
                    System.out.println(Thread.currentThread().getName() + ": Further transforming...");
                    return s.toUpperCase(); // Result: HELLO WORLD
                });

            System.out.println("Chained result: " + chainedFuture.get()); // Blocks for final result


            // --- 4. Combining multiple futures with allOf ---
            System.out.println("\n--- Combining with allOf ---");
            CompletableFuture<Void> allFutures = CompletableFuture.allOf(
                CompletableFuture.runAsync(() -> {
                    try { Thread.sleep(500); } catch (InterruptedException e) { Thread.currentThread().interrupt(); }
                    System.out.println("Task A Done");
                }),
                CompletableFuture.runAsync(() -> {
                    try { Thread.sleep(1000); } catch (InterruptedException e) { Thread.currentThread().interrupt(); }
                    System.out.println("Task B Done");
                }),
                CompletableFuture.runAsync(() -> {
                    try { Thread.sleep(700); } catch (InterruptedException e) { Thread.currentThread().interrupt(); }
                    System.out.println("Task C Done");
                })
            );

            // allOf returns CompletableFuture<Void>, use join() to wait for all
            allFutures.join(); // Blocks until all tasks A, B, C are done
            System.out.println("All tasks (A, B, C) completed!");


            // --- 5. Timeout handling ---
            System.out.println("\n--- Timeout Handling ---");
            CompletableFuture<String> timeoutFuture = CompletableFuture.supplyAsync(() -> {
                try {
                    Thread.sleep(3000); // This task takes 3 seconds
                } catch (InterruptedException e) {
                    Thread.currentThread().interrupt();
                }
                return "Long Task Done";
            }).orTimeout(1, TimeUnit.SECONDS); // Timeout after 1 second

            try {
                System.out.println("Result with timeout: " + timeoutFuture.get()); // Will throw TimeoutException
            } catch (Exception e) {
                System.out.println("Exception occurred: " + e.getCause()); // Output: java.util.concurrent.TimeoutException
            }


            // --- 6. Handling exceptions ---
            System.out.println("\n--- Exception Handling ---");
            CompletableFuture<String> errorFuture = CompletableFuture.supplyAsync(() -> {
                if (true) {
                    throw new RuntimeException("Something went wrong!"); // Simulate error
                }
                return "Never reached";
            }).exceptionally(ex -> { // Handles exception
                System.out.println("Caught exception: " + ex.getMessage());
                return "Recovered from error"; // Provides a fallback value
            });

            System.out.println("Result from error future: " + errorFuture.get()); // Output: Recovered from error


            // Important: Shuts down any default Executor used by CompletableFuture
            // Not strictly needed for commonPool, but good practice if using custom executors
            // In a real application, you'd manage your own ExecutorService and pass it to supplyAsync/runAsync
            // e.g., CompletableFuture.supplyAsync(supplier, myExecutorService);
        }
    }
    ```
    *   **Explanation**: This comprehensive example illustrates various features of `CompletableFuture`: asynchronous execution, blocking/non-blocking result retrieval, chaining dependent operations, waiting for multiple futures, and handling timeouts and exceptions.

---

### Conclusion and Analogy

Java Multithreading is a challenging but crucial topic for modern software development, enabling applications to efficiently use CPU resources and be more responsive. It moves beyond sequential execution to parallel and concurrent processing.

**Analogy for Multithreading:**

Imagine you are a master chef (the **CPU**) in a very busy restaurant (your **computer**).

*   **Single-Core CPU**: In an old kitchen, you (the chef) can only cook one dish at a time. To handle multiple orders (processes), you quickly switch between different dishes – chop vegetables for one, stir the sauce for another, flip a pancake for a third. It looks like you're doing everything at once, but you're just very fast at **"context switching"** (multitasking on a single core).

*   **Multi-Core CPU**: Now, your kitchen has multiple cooking stations (cores), and you've hired assistant chefs (more cores). You can assign different dishes to different assistants, or even different parts of the same complex dish to different assistants. All of them are cooking *truly at the same time* (true parallel execution).

*   **Program**: The entire restaurant's menu book is your program (set of instructions).
*   **Process**: When a customer places an order for a "combo meal," that order becomes a process. It's a running instance of a menu item.
*   **Thread**: A "combo meal" (process) involves several components: cooking the main course, preparing the side salad, and making the drink. Each of these individual tasks is a "thread". You (or your assistants) can work on these parts concurrently.
*   **Synchronization (`synchronized` / Locks)**: Sometimes, multiple assistants need to use the *same cutting board* (a shared resource like a shared variable) or the *same special spice jar* (a critical section). To prevent chaos (race conditions) where ingredients get mixed up, you put a **"lock"** on the cutting board. Only one assistant can use it at a time (mutual exclusion).
*   **Deadlock**: Imagine one assistant holds the special knife and needs the cutting board, while another assistant holds the cutting board and needs the special knife. Both are stuck, waiting for each other indefinitely – that's a deadlock. You'd resolve this by setting a rule: "Always get the cutting board *before* the special knife!" (consistent lock ordering).
*   **Thread Communication (`wait()`, `notify()`):** The "salad chef" (consumer thread) needs to wait for the "main course chef" (producer thread) to finish cooking the chicken before preparing the salad. Instead of constantly checking if the chicken is ready (busy waiting), the main course chef can just shout "Chicken is done!" (`notify()`) when it's ready, and the salad chef, who was resting (`wait()`), can then start.
*   **Executor Framework (Thread Pools)**: Instead of hiring a new chef for every single order that comes in and firing them once the order is done (manual thread management), you have a **"pool of ready-to-cook chefs"** always available in the kitchen. When an order comes, you assign it to the next available chef from the pool. This saves time and resources in hiring and firing.
*   **CompletableFuture**: If a customer places a very complex order that involves several steps that can be done independently or sequentially, you might jot down "once main course is ready, then add sauce, then garnish". You don't have to stand there watching each step; you just define the *flow* of tasks, and they happen asynchronously. You can even check in later to `get()` the final result, or define what to do `thenApply()` it to something else, or `exceptionally()` if something goes wrong.

Just like a well-managed kitchen ensures delicious food is served efficiently, well-managed multithreading ensures your applications run smoothly and perform optimally.
