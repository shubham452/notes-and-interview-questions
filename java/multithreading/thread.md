Here are notes with examples on how to create new threads in Java, based on the provided sources:

To create a new thread in Java, you can use one of two primary methods: **extending the `Thread` class** or **implementing the `Runnable` interface**.

### 1. Extending the `Thread` Class

This method involves creating a new class that inherits from Java's built-in `Thread` class.

*   **Steps:**
    1.  **Create a new class and extend `Thread`**: Define a class (e.g., `World`) and make it extend the `Thread` class.
        *   Example: `class World extends Thread { ... }`
    2.  **Override the `run()` method**: Inside your new class, override the `run()` method. This method is where you write the code (your "story" or "work") that you want to execute in the new thread.
        *   Example:
            ```java
            class World extends Thread {
                @Override
                public void run() {
                    for (int i = 0; i < 10000; i++) {
                        System.out.println("World"); // Or Thread.currentThread().getName()
                    }
                }
            }
            ```
           
    3.  **Initiate the thread**: In your main thread (e.g., in the `main` method), create an object of your new class (e.g., `World`) and then call its `start()` method.
        *   Example:
            ```java
            public static void main(String[] args) {
                World worldObject = new World(); // Create an object of your thread class
                worldObject.start();             // Call the start method to begin execution in a new thread
                // ... code for main thread (e.g., System.out.println("Hello");)
            }
            ```
           
*   **Behavior and Observations:**
    *   Calling `start()` **initiates the thread** and invokes the `run()` method.
    *   When multiple threads are running (e.g., a `World` thread and the `main` thread printing "Hello"), their execution order will be **random** and **not sequential**. You might see "Hello World Hello World" or "World World Hello Hello" or any other intermingling. This is because they are two independent tasks.
    *   You can use `Thread.currentThread().getName()` within the `run()` method or the main thread to see which thread is currently executing. For example, the main thread will print "main", and automatically created threads might be named "Thread-0", "Thread-1", etc..

### 2. Implementing the `Runnable` Interface

This method involves creating a new class that implements the `Runnable` interface.

*   **Steps:**
    1.  **Create a new class and implement `Runnable`**: Define a class (e.g., `World`) and make it implement the `Runnable` interface.
        *   Example: `class World implements Runnable { ... }`
    2.  **Override the `run()` method**: Similar to extending `Thread`, you must override the `run()` method in your new class to define the code that will be executed in the new thread.
        *   Example:
            ```java
            class World implements Runnable {
                @Override
                public void run() {
                    for (int i = 0; i < 10000; i++) {
                        System.out.println("World");
                    }
                }
            }
            ```
           
    3.  **Initiate the thread**: This method requires an additional step compared to extending `Thread`. You first create an instance of your `Runnable` class, then create a `Thread` object, passing your `Runnable` instance to the `Thread` constructor. Finally, you call the `start()` method on the `Thread` object.
        *   Example:
            ```java
            public static void main(String[] args) {
                World worldRunnable = new World();    // Create an instance of your Runnable class
                Thread t1 = new Thread(worldRunnable); // Create a Thread object, passing the Runnable instance
                t1.start();                          // Call the start method on the Thread object
                // ... code for main thread (e.g., System.out.println("Hello");)
            }
            ```
           
*   **Behavior and Observations:**
    *   Similar to the `Thread` class extension, this approach also results in **parallel execution** where "Hello" and "World" (or whatever tasks are defined) will print randomly, showing that both threads are running concurrently.
    *   This is generally the **preferred method** because Java does not support multiple inheritance for classes, meaning a class can only extend one other class. By implementing `Runnable`, your class can still extend another class while also defining thread behavior.
