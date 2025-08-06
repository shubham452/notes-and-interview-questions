Here are notes on locking mechanisms in Java, drawing from the provided sources:

### Introduction to Locking

*   **The Problem of Shared Resources**: When multiple "threads" (like children in an example) try to access and modify a "shared resource" (like a notebook) simultaneously without coordination, it can lead to chaotic, "jumbled," and "messed up" results, making it difficult to understand what happened. This is because multiple threads might try to write to the same line at the same time, or one thread might read incomplete data that another thread is in the process of writing.
*   **The Solution: Locking (Synchronization)**: To prevent this chaos and ensure that only one thread accesses the shared resource at a time, "locking" mechanisms are used. This ensures that operations on shared resources are performed in an orderly manner, leading to correct and predictable output. For instance, if a `synchronized` keyword is used on a shared notebook, only one person can access it at a time. When one thread accesses a resource, it "applies a lock" so no other thread can access it. Once its work is done, or its turn ends (like a CPU scheduler or teacher decides), the lock is passed to the next thread.

### Types of Locks

There are two main types of locks in Java:

1.  **Intrinsic Locks (Automatic/Implicit)**:
    *   **Mechanism**: These are built into every Java object, though not explicitly visible. When you use the `synchronized` keyword, you are essentially utilizing these intrinsic locks.
    *   **Control**: They are "automatic" and activated simply by using `synchronized`. You don't have direct control over *how* or *when* the lock is acquired or released beyond the scope of the `synchronized` block or method.
    *   **Example**: In the bank account example, applying `synchronized` to the `withdraw` method ensures that when `t1` accesses it, `t2` cannot access it until `t1` completes its operation, including any `Thread.sleep()` duration.
    *   **Limitation**: A significant limitation is that if a thread holds an intrinsic lock for an extended period (e.g., due to a long `Thread.sleep()` or database operation), other waiting threads are "indefinitely waiting" and cannot be interrupted or explicitly told to try again later. This can lead to a thread waiting for an hour or more, unaware of potential issues.

2.  **Explicit Locks (Manual)**:
    *   **Mechanism**: These are more advanced and provide greater control over locking behavior. They are managed using the `Lock` interface, typically implemented by classes like `ReentrantLock` found in `java.util.concurrent.locks`.
    *   **Control**: With explicit locks, you have manual control over *when* to lock and *when* to unlock. This gives you more power to define how and when threads can access a shared resource.
    *   **Benefits**: They offer mechanisms to prevent indefinite waits and allow for more sophisticated locking strategies, such as attempting to acquire a lock for a specific duration or handling interruptions.

### `ReentrantLock` and its Methods

`ReentrantLock` is a class that implements the `Lock` interface, providing explicit locking capabilities.

*   **Creating a Lock Object**: You create an instance of `ReentrantLock` as a private, final field in your class, for example: `private final Lock lock = new ReentrantLock();`. This lock object is then used to control access to critical sections.

Here are some key methods of the `ReentrantLock` class:

*   **`lock()` Method**:
    *   **Function**: This method acquires the lock. If the lock is not available (i.e., another thread holds it), the current thread will **wait indefinitely** until the lock becomes available.
    *   **Similarity**: It behaves similarly to the `synchronized` keyword in terms of waiting behavior.
    *   **Use Case**: Use when a thread *must* acquire the lock and can afford to wait indefinitely.
    *   **Limitation**: Does not allow for interruption while waiting, similar to intrinsic locks.

*   **`tryLock()` Method**:
    *   **Function**: Attempts to acquire the lock **only if it is free at the time of invocation**. It does not wait.
    *   **Return Value**: Returns `true` if the lock was acquired, `false` otherwise.
    *   **Benefit**: Prevents indefinite waiting. If the lock is not available, the thread can immediately proceed to an `else` block or try again later, rather than blocking.
    *   **Example**: In the bank account example, if `t1` holds the lock, `t2` executing `tryLock()` will immediately return `false` if the lock isn't free, allowing `t2` to print "Could not acquire the lock. Will try again later" instead of waiting.

*   **`tryLock(long timeout, TimeUnit unit)` Method**:
    *   **Function**: Attempts to acquire the lock within a **specified waiting time**. The current thread will wait for the given duration.
    *   **Return Value**: Returns `true` if the lock is acquired within the waiting time, `false` if the timeout expires or the thread is interrupted.
    *   **Benefit**: Provides a controlled waiting period, preventing indefinite waits. If the lock isn't acquired within the specified time, the thread can take alternative actions.
    *   **Exception Handling**: This method can throw an `InterruptedException` if the current thread is interrupted while waiting for the lock, thus requiring a `try-catch` block.

*   **`lockInterruptibly()` Method**:
    *   **Function**: Acquires the lock **unless the current thread is interrupted**.
    *   **Benefit**: Unlike `lock()`, this method allows a waiting thread to be interrupted, preventing it from being indefinitely blocked.
    *   **Exception Handling**: Throws an `InterruptedException` if the thread is interrupted while waiting.

*   **`unlock()` Method**:
    *   **Function**: Releases the lock that was previously acquired by the current thread.
    *   **Crucial Practice**: It is **essential to call `unlock()` in a `finally` block** to ensure the lock is always released, even if exceptions occur during the critical section. Failing to release the lock can lead to deadlocks or other threads being permanently blocked.

#### Example: Bank Account Withdrawal with `ReentrantLock`

Instead of `synchronized`, `ReentrantLock` provides fine-grained control:

```java
// Inside the BankAccount class
private final Lock lock = new ReentrantLock();
private int balance = 100;

public void withdraw(int amount) {
    try {
        // Attempt to acquire the lock, waiting for a maximum of 1 second
        if (lock.tryLock(1000, TimeUnit.MILLISECONDS)) { //
            try {
                // Critical section starts here
                if (balance >= amount) { //
                    System.out.println(Thread.currentThread().getName() + " proceeding with withdrawal."); //
                    Thread.sleep(3000); // Simulate transaction processing
                    balance -= amount; //
                    System.out.println(Thread.currentThread().getName() + " completed withdrawal. Remaining Balance: " + balance); //
                } else {
                    System.out.println(Thread.currentThread().getName() + " insufficient balance."); //
                }
            } finally {
                // Ensure the lock is always released
                lock.unlock(); //
            }
        } else {
            // Lock was not acquired within 1 second
            System.out.println(Thread.currentThread().getName() + " could not acquire the lock. Will try again later."); //
        }
    } catch (InterruptedException e) {
        // Handle interruption while waiting for the lock
        System.out.println(Thread.currentThread().getName() + " was interrupted while waiting for the lock.");
        Thread.currentThread().interrupt(); // Restore interrupted status
    }
}
```

*   When `t1` attempts to withdraw, it acquires the lock and processes for 3 seconds.
*   When `t2` attempts to withdraw, `tryLock(1000, TimeUnit.MILLISECONDS)` is called. Since `t1` holds the lock for 3 seconds, `t2`'s 1-second waiting period will expire, and `tryLock` will return `false`.
*   Consequently, `t2` will print "Could not acquire the lock. Will try again later" and will **not wait indefinitely**, unlike with `synchronized`. This demonstrates greater control and prevents one thread from blocking another for an unknown duration.

#### Reentrancy of `ReentrantLock`

*   **Definition**: The term "Reentrant" means that a thread that already holds a lock can **re-enter** any code section protected by the **same lock** without getting deadlocked. It's like having the main key to your house; once you're in, you can open any other room within that house without needing another key or waiting for yourself to "unlock" the main door.
*   **How it Works**: `ReentrantLock` maintains an **internal count** of how many times the lock has been acquired by the current thread.
    *   When a thread acquires the lock for the first time, the count is 1.
    *   If the *same thread* calls `lock()` again (e.g., an outer method calls an inner method, and both are protected by the same lock), the count increments (e.g., to 2).
    *   The lock is **not actually released** until the `unlock()` method has been called an equal number of times as `lock()` was called, effectively decrementing the count back to zero.
*   **Deadlock Prevention**: Without reentrancy, if an `outerMethod` acquires a lock and then calls an `innerMethod` which tries to acquire the *same lock* again, it would lead to a deadlock because the inner method would wait for the outer method to release the lock, which it can't do until the inner method finishes. `ReentrantLock` prevents this by allowing the same thread to acquire the lock multiple times.
*   **Example (`ReentrantExample`)**:
    ```java
    class ReentrantExample {
        private final Lock lock = new ReentrantLock(); //

        public void outerMethod() {
            lock.lock(); // First acquisition
            try {
                System.out.println("Outer Method"); //
                innerMethod(); // Calls inner method
            } finally {
                lock.unlock(); // Release for outer method
            }
        }

        public void innerMethod() {
            lock.lock(); // Second acquisition by the same thread
            try {
                System.out.println("Inner Method"); //
            } finally {
                lock.unlock(); // Release for inner method
            }
        }
    }
    ```
    When `outerMethod` is called, it acquires the lock (count becomes 1). It then calls `innerMethod`. Since `innerMethod` tries to acquire the *same lock* by the *same thread*, the lock count simply increases (to 2) instead of causing a deadlock. The lock is only fully released when both `unlock()` calls have been executed, bringing the count back to zero.

#### Handling Interrupted Exceptions

*   **Importance**: When a method capable of throwing `InterruptedException` (like `tryLock(long timeout, TimeUnit unit)` or `lockInterruptibly()`) is called, it's not enough to just catch the exception and log it.
*   **Restoring Interrupted Status**: You must either **re-throw the `InterruptedException`** or, if you're handling it locally, **restore the interrupted status of the current thread** by calling `Thread.currentThread().interrupt()`.
*   **Reason**: Failing to restore the interrupted status means that information about the thread being interrupted is lost. This can delay thread shutdown and prevent higher-level monitoring code or subsequent operations that check for interruption status (e.g., `Thread.currentThread().isInterrupted()`) from properly handling the situation. Restoring the status allows other parts of the code to react to the interruption, possibly by performing cleanup or stopping execution.
