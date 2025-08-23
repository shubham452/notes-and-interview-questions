Here are comprehensive notes on the **Java Executor Framework** with coding examples, drawing from the provided YouTube source:

### Notes on Java Executor Framework

**1. Introduction to Executor Framework**

*   The **Executor Framework** was introduced in **Java 5**.
*   Its primary purpose is to **simplify the development of concurrent applications** (multi-threading) by **abstracting away many complexities** involved in manually creating and managing threads.
*   **Before the Executor Framework**, developers had to **manually create and manage threads**. This led to several problems:
    *   **Manual Thread Management:** Similar to having to manually call friends for help (lemonade analogy), there was no predefined system, leading to poor resource management.
    *   **Overhead of Thread Creation/Destruction:** Creating and destroying threads for every task is an expensive operation that consumes memory and processor resources.
    *   **Lack of Scalability:** Without thread pooling, the system might crash under heavy load (many requests).
    *   **Error Handling Complexity:** Manual thread creation and management increase the complexity of the code, making error handling more difficult and increasing the chances of errors.
*   The Executor Framework handles the thread management, allowing developers to focus on the **business logic** rather than the intricacies of threading.

**2. Core Interfaces of Executor Framework**

The Executor Framework primarily revolves around three core interfaces:
*   **`Executor`**: The most basic interface, with a single `execute(Runnable command)` method. It doesn't offer control over thread lifecycle (like shutdown).
*   **`ExecutorService`**: Extends `Executor` and provides more advanced features for managing the lifecycle of tasks and the executor itself. This is the most commonly used interface for managing thread pools.
*   **`ScheduledExecutorService`**: Extends `ExecutorService` and provides methods for scheduling tasks to run after a delay or periodically.

**3. Implementing Multithreading with and without ExecutorService (Factorial Example)**

The video uses a factorial calculation example to demonstrate the benefits of the Executor Framework. The task is to calculate factorials for numbers 1 to 10. The factorial calculation is simulated as a heavy computational task using `Thread.sleep(1000)` (1 second).

*   **Synchronous Execution (without Multithreading):**
    *   Calculating factorials for 1 to 10 synchronously takes approximately **9 seconds** (9086 milliseconds).

    ```java
    // Example conceptual code (from source description)
    // for (int i = 1; i <= 10; i++) {
    //     long result = factorial(i); // factorial method has Thread.sleep(1000)
    //     System.out.println("Factorial of " + i + " is " + result);
    // }
    // This runs sequentially, taking about 9-10 seconds for 10 factorials.
    ```

*   **Manual Multithreading (without Executor Framework):**
    *   Creating 10 separate threads and starting them.
    *   **Problem:** Without waiting for all threads to complete, the `total time` calculation in the main thread will be incorrect, as it measures only thread creation time, not execution time.
    *   **Solution:** Use `thread.join()` for each thread to make the main thread wait for all worker threads to finish.

    ```java
    // Example code (from source)
    long startTime = System.currentTimeMillis();

    // Create an array of Threads
    Thread[] threads = new Thread;

    for (int i = 1; i <= 10; i++) {
        // Lambda expression for Runnable task
        final int num = i; // num is effectively final for lambda
        threads[i - 1] = new Thread(() -> {
            long result = factorial(num); // Assuming factorial method exists
            System.out.println("Factorial of " + num + " is " + result);
        });
        threads[i - 1].start(); // Start each thread
    }

    // Wait for all threads to complete using join()
    for (int i = 0; i < 10; i++) {
        try {
            threads[i].join();
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
        }
    }

    long totalTime = System.currentTimeMillis() - startTime;
    System.out.println("Total Time: " + totalTime + " ms");
    // With this, the time reduces to ~1 second for 10 factorials.
    ```
    *   **Disadvantages of Manual Multithreading**:
        *   **No Thread Reuse**: New threads are created for each task.
        *   **Manual Thread Management**: Developers handle thread creation, starting, and waiting explicitly.

*   **Multithreading with `ExecutorService` (The Recommended Approach):**
    *   **Executor Framework** handles thread creation and management internally, allowing the developer to focus on the business logic.
    *   **Thread Reuse**: Threads in the pool are reused for multiple tasks.

    ```java
    // Example code (from source)
    long startTime = System.currentTimeMillis();

    // Create an ExecutorService with a fixed-size thread pool (e.g., 3 threads)
    // Executors is a utility class for creating ExecutorService instances.
    ExecutorService executor = Executors.newFixedThreadPool(3); // 3 threads in the pool

    for (int i = 1; i <= 10; i++) {
        final int num = i; // Effectively final variable for lambda
        executor.submit(() -> { // submit() takes a Runnable task
            long result = factorial(num);
            System.out.println("Factorial of " + num + " is " + result);
        });
    }

    // Shut down the executor. It stops accepting new tasks and finishes existing ones.
    executor.shutdown();

    // To wait for all tasks to complete, use awaitTermination().
    try {
        // Wait for up to 100 seconds for all tasks to complete.
        executor.awaitTermination(100, TimeUnit.SECONDS);
    } catch (InterruptedException e) {
        Thread.currentThread().interrupt();
    }

    long totalTime = System.currentTimeMillis() - startTime;
    System.out.println("Total Time: " + totalTime + " ms");
    // With 3 threads, it might take ~3 seconds for 10 factorials.
    // With 10 threads, it would take ~1 second, similar to manual multithreading but with thread reuse.
    ```

**4. `ExecutorService` Methods and Concepts**

*   **`Executors` Utility Class**: Provides static factory methods to create different types of `ExecutorService` instances.
    *   `Executors.newFixedThreadPool(int nThreads)`: Creates a thread pool with a fixed number of threads.
    *   `Executors.newSingleThreadExecutor()`: Creates an executor that uses a single worker thread.
    *   `Executors.newCachedThreadPool()`: Creates a thread pool that creates new threads as needed, but reuses previously constructed threads when they are available. Threads that have been inactive for 60 seconds are terminated. (See more details in "Utility Methods" section).
    *   `Executors.newScheduledThreadPool(int corePoolSize)`: Creates a thread pool that can schedule commands to run after a given delay, or to execute periodically. (See more details in "ScheduledExecutorService" section).

*   **`submit(Runnable task)`**: Submits a `Runnable` task for execution. It returns a `Future<?>` object.
*   **`shutdown()`**: Initiates an **orderly shutdown**. It prevents new tasks from being submitted but allows previously submitted tasks to complete. The main thread **does not wait** for the tasks to finish after `shutdown()`.
*   **`awaitTermination(long timeout, TimeUnit unit)`**: Blocks until all tasks have completed execution after a `shutdown` request, or the timeout occurs, or the current thread is interrupted, whichever happens first. This is used to make the main thread wait for the executor's tasks to complete.
    *   You can set an unlimited wait with a `while(!executor.awaitTermination(1, TimeUnit.MILLISECONDS))` loop.
*   **`shutdownNow()`**: Attempts to stop all actively executing tasks, halts the processing of waiting tasks, and returns a list of the tasks that were awaiting execution. It's an immediate, forceful shutdown, and tasks might not complete.
    *   **Example**: If `shutdownNow()` is called immediately after submitting tasks, nothing might print.
*   **`isShutdown()`**: Returns `true` if this executor has been shut down.
*   **`isTerminated()`**: Returns `true` if all tasks have completed following a `shutdown` request. This is often used with a small delay to ensure completion.

    ```java
    // Example of isShutdown and isTerminated
    ExecutorService executorService = Executors.newFixedThreadPool(2);
    // ... submit tasks ...
    executorService.shutdown();
    System.out.println("Is Shutdown: " + executorService.isShutdown()); // true

    // Give some time for tasks to complete
    try {
        Thread.sleep(1000); // 1 second delay
    } catch (InterruptedException e) {
        Thread.currentThread().interrupt();
    }
    System.out.println("Is Terminated after delay: " + executorService.isTerminated()); // true if tasks finished
    ```

**5. `Future` Interface: Handling Task Results and Status**

When you submit a task using `executor.submit()`, it returns a `Future` object. `Future` represents the result of an asynchronous computation.

*   **`Future<?> future = executor.submit(task)`**: The `Future` object allows you to check if the task is done, wait for its completion, and retrieve its result.
*   **`Future.get()`**: **Blocks** until the task completes and then retrieves its result. If the task was submitted with a `Runnable` (which doesn't return a value), `get()` will return `null`. If the task was submitted with a `Callable` (which returns a value), `get()` will return that value.
    *   **Example (with `Callable`):**
        ```java
        ExecutorService singleThreadExecutor = Executors.newSingleThreadExecutor();
        // Callable that returns 42
        Future<Integer> futureResult = singleThreadExecutor.submit(() -> 42); // returns 42

        try {
            Integer result = futureResult.get(); // Main thread waits here and gets 42
            System.out.println("Result: " + result); // Output: Result: 42
        } catch (InterruptedException | ExecutionException e) {
            e.printStackTrace();
        } finally {
            singleThreadExecutor.shutdown();
        }
        ```
*   **`Future.isDone()`**: Returns `true` if the task completed. Completion can be due to normal termination, an exception, or cancellation. It **does not block**.
    *   **Example:**
        ```java
        // ... (using futureResult from above)
        System.out.println("Is Done before get(): " + futureResult.isDone()); // Likely false if task is long
        // futureResult.get(); // If we call get() here, it will wait
        System.out.println("Is Done after get(): " + futureResult.isDone()); // True
        ```
*   **`Future.get(long timeout, TimeUnit unit)`**: Waits for the task to complete for a specified `timeout` duration. If the task doesn't complete within the timeout, it throws a `TimeoutException`.
    *   **Example:**
        ```java
        ExecutorService executor = Executors.newSingleThreadExecutor();
        Future<Integer> future = executor.submit(() -> {
            try {
                Thread.sleep(2000); // Task takes 2 seconds
            } catch (InterruptedException e) {
                Thread.currentThread().interrupt();
            }
            return 42;
        });

        try {
            // Wait only 1 second for a 2-second task
            Integer result = future.get(1, TimeUnit.SECONDS); // Throws TimeoutException
            System.out.println("Result: " + result);
        } catch (InterruptedException | ExecutionException | TimeoutException e) {
            System.out.println("Exception occurred: " + e.getMessage()); // Output: Exception occurred: java.util.concurrent.TimeoutException
        } finally {
            executor.shutdownNow(); // Important to shut down if timeout occurs
        }
        ```
*   **`Future.cancel(boolean mayInterruptIfRunning)`**: Attempts to cancel the execution of this task.
    *   `mayInterruptIfRunning = true`: Attempts to interrupt the task if it's currently running.
    *   `mayInterruptIfRunning = false`: Will not interrupt a running task; it will only prevent a task that has not started yet from running.
    *   **Example:**
        ```java
        ExecutorService executor = Executors.newSingleThreadExecutor();
        Future<String> future = executor.submit(() -> {
            try {
                Thread.sleep(2000); // Task takes 2 seconds
                System.out.println("Hello from Task"); // This will print if not interrupted/cancelled
                return "Task Completed";
            } catch (InterruptedException e) {
                Thread.currentThread().interrupt();
                return "Task Interrupted";
            }
        });

        try {
            Thread.sleep(100); // Give the task a moment to start
            boolean cancelled = future.cancel(true); // Attempt to cancel and interrupt if running
            System.out.println("Task Cancelled: " + cancelled);
            System.out.println("Is Cancelled: " + future.isCancelled()); // True
            System.out.println("Is Done: " + future.isDone()); // True (due to cancellation)
            future.get(); // This will throw a CancellationException
        } catch (InterruptedException | ExecutionException e) {
            System.out.println("Exception on get(): " + e.getMessage()); // Output will show CancellationException
        } finally {
            executor.shutdownNow();
        }
        ```
*   **`Future.isCancelled()`**: Returns `true` if the task was cancelled before it completed normally.

**6. `Runnable` vs. `Callable`**

These are the two main interfaces used to define tasks for the Executor Framework.

*   **`Runnable`**:
    *   Used when a task **does not need to return a result**.
    *   Its single abstract method is `void run()`.
    *   The `run()` method **cannot directly throw checked exceptions** (like `InterruptedException`), so `try-catch` blocks are required for exceptions within the `run()` method.
    *   **Example**:
        ```java
        Runnable runnableTask = () -> System.out.println("This task doesn't return anything.");
        // Submit using executor.submit(runnableTask)
        ```

*   **`Callable<V>`**:
    *   Used when a task **needs to return a result**. `V` is the type of the result.
    *   Its single abstract method is `V call() throws Exception`.
    *   The `call()` method **can throw checked exceptions**, making exception handling cleaner (can declare `throws Exception` in the lambda/method signature).
    *   **Example**:
        ```java
        Callable<String> callableTask = () -> {
            Thread.sleep(100); // Can directly throw InterruptedException
            return "This task returns a String.";
        };
        // Submit using Future<String> future = executor.submit(callableTask);
        ```
    *   When `executor.submit()` is used with a lambda expression that returns a value, the `Callable` version of `submit` is implicitly called, and it returns a `Future` typed with the return value.

**7. `ScheduledExecutorService`: Scheduling Tasks**

`ScheduledExecutorService` allows you to execute tasks after a delay or periodically.

*   **Creating a `ScheduledExecutorService`**:
    *   `ScheduledExecutorService scheduler = Executors.newScheduledThreadPool(1);` (Creates a pool with 1 thread for scheduling).

*   **`schedule(Runnable command, long delay, TimeUnit unit)`**: Schedules a one-time task to run after a specified `delay`.
    *   **Example**:
        ```java
        ScheduledExecutorService scheduler = Executors.newScheduledThreadPool(1);
        Runnable task = () -> System.out.println("Task executed after 5 second delay");
        scheduler.schedule(task, 5, TimeUnit.SECONDS); // Run once after 5 seconds
        scheduler.shutdown(); // Shuts down after the scheduled task completes
        ```

*   **`scheduleAtFixedRate(Runnable command, long initialDelay, long period, TimeUnit unit)`**: Schedules a periodic task to execute repeatedly. The `period` parameter specifies the time between the *start* of successive executions, regardless of how long the task itself takes.
    *   **Example**:
        ```java
        ScheduledExecutorService scheduler = Executors.newScheduledThreadPool(1);
        Runnable periodicTask = () -> System.out.println("Task executed every 5 seconds (fixed rate)");
        // Initial delay of 5 seconds, then every 5 seconds
        scheduler.scheduleAtFixedRate(periodicTask, 5, 5, TimeUnit.SECONDS);

        // To stop a periodic task, you need to explicitly shut down the scheduler
        // or cancel the returned ScheduledFuture.
        // For demonstration, let's shut down after 20 seconds.
        scheduler.schedule(() -> { // Schedule another task to shut down the scheduler
            System.out.println("Initiating shutdown...");
            scheduler.shutdown();
        }, 20, TimeUnit.SECONDS); // Shutdown after 20 seconds

        // This will print "Task executed every 5 seconds (fixed rate)" 4 times (at ~5s, 10s, 15s, 20s).
        ```

*   **`scheduleWithFixedDelay(Runnable command, long initialDelay, long delay, TimeUnit unit)`**: Schedules a periodic task where the `delay` parameter specifies the time between the *end* of one execution and the *start* of the next. This ensures a fixed pause between task runs, preventing overlap if a task takes longer than its period.
    *   **Example**:
        ```java
        // Similar to scheduleAtFixedRate, but the 5-second delay starts AFTER the previous task finishes.
        // scheduler.scheduleWithFixedDelay(task, 5, 5, TimeUnit.SECONDS);
        ```

**8. Advanced `ExecutorService` Methods**

*   **`invokeAll(Collection<? extends Callable<T>> tasks)`**: Executes all given tasks and returns a `List<Future<T>>` containing the status and results of all tasks **when all have completed**.
    *   This method **blocks** until all tasks are completed.
    *   **Example**:
        ```java
        ExecutorService executor = Executors.newFixedThreadPool(2);
        List<Callable<Integer>> callables = new ArrayList<>();
        callables.add(() -> { Thread.sleep(1000); System.out.println("Task 1"); return 1; });
        callables.add(() -> { Thread.sleep(500); System.out.println("Task 2"); return 2; });
        callables.add(() -> { Thread.sleep(1500); System.out.println("Task 3"); return 3; });

        try {
            // invokeAll blocks until all tasks are done
            List<Future<Integer>> futures = executor.invokeAll(callables); //
            System.out.println("Hello World (after all tasks)"); // This prints last
            for (Future<Integer> f : futures) {
                System.out.println("Result: " + f.get()); // Get results of each future
            }
        } catch (InterruptedException | ExecutionException e) {
            e.printStackTrace();
        } finally {
            executor.shutdown();
        }
        ```
    *   `invokeAll` also has an overloaded version that accepts a `timeout`, cancelling incomplete tasks after the timeout.

*   **`invokeAny(Collection<? extends Callable<T>> tasks)`**: Executes the given tasks, returning the result of **one that completes successfully first**. Other tasks are cancelled.
    *   This method **blocks** until one task completes or an exception is thrown.
    *   It returns the result directly, not a `Future`.
    *   **Example**:
        ```java
        ExecutorService executor = Executors.newFixedThreadPool(3);
        List<Callable<Integer>> callables = new ArrayList<>();
        callables.add(() -> { Thread.sleep(2000); System.out.println("Task A"); return 10; });
        callables.add(() -> { Thread.sleep(500); System.out.println("Task B"); return 20; }); // This one will finish first
        callables.add(() -> { Thread.sleep(3000); System.out.println("Task C"); return 30; });

        try {
            Integer result = executor.invokeAny(callables); // Returns result of the first completed task
            System.out.println("First completed result: " + result); // Output: First completed result: 20
        } catch (InterruptedException | ExecutionException e) {
            e.printStackTrace();
        } finally {
            executor.shutdown();
        }
        ```

**9. Types of Thread Pools in `Executors` Utility Class (Revisited)**

*   **`Executors.newFixedThreadPool(int nThreads)`**:
    *   Creates a thread pool with a **fixed number of threads**.
    *   If more tasks are submitted than available threads, the extra tasks wait in a queue.
    *   **Use case**: When you know the maximum number of concurrent tasks and want to manage resource consumption.

*   **`Executors.newSingleThreadExecutor()`**:
    *   A specialized `FixedThreadPool` with **only one thread**.
    *   Guarantees that tasks are executed sequentially.
    *   **Use case**: When you need to ensure tasks are processed in order, or for background operations that don't require high concurrency.

*   **`Executors.newCachedThreadPool()`**:
    *   Creates a thread pool that **dynamically adjusts its size**.
    *   It creates new threads as needed (if no idle threads are available).
    *   It reuses existing idle threads.
    *   Threads that have been inactive for **60 seconds** are terminated and removed from the pool.
    *   **Risk**: No upper limit on the number of threads, which can exhaust system resources if tasks are long-lived and load is high.
    *   **Use cases**:
        *   When the **load is variable** (unpredictable number of tasks).
        *   When tasks are **short-lived**.
        *   It manages concurrent spikes well by quickly increasing the pool size, and then reduces it during inactive periods.

This concludes the detailed notes on the Java Executor Framework based on the provided video source.
