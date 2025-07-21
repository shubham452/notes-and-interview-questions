Here are detailed notes on the Java Collections Framework and Streams, drawing from the provided sources, along with coding examples to enhance your understanding:

### 1. Introduction to Java Collections Framework

*   A **Collection** is fundamentally a group of elements. We use this term daily, like a collection of coins or bottle caps. In Java, collections typically store **strings, numbers, or objects**.
*   The **Collection Framework** in Java consists of **classes and interfaces** that help manage these collections.
*   **Before Java version 2 (or Java 1.2)**, Java relied on classes like `Vector`, `Stack`, `Hashtable`, and arrays to manipulate groups of objects.
*   However, these older classes had **drawbacks**:
    *   **Inconsistencies**: Each class had its own management style, leading to confusion and difficulty in remembering things.
    *   **Lack of common interface**: They didn't work together, making it hard to write **generic methods or define generic variables**.
    *   **Interoperability issues**: They were independent classes, leading to many problems.
*   The **Collection Framework** was introduced in **Java version 2 (or 1.2)** to solve these problems. It brought **interoperability**, allowing interchangeable use of components, and **interfaces** for writing generic methods and variables.

### 2. Key Interfaces in Collections Framework

The Collection Framework has many key interfaces, which are the root interfaces, along with their implementing classes.
*   **Collection**: This is the **root interface** for all collection interfaces.
*   **List**: Represents an **ordered collection** (sequence) that can contain **duplicate elements**. Similar to arrays in how elements are stored and accessed.
*   **Set**: Represents a collection that **does not allow duplicate elements**. Elements are generally **unordered**.
*   **Queue**: Follows the **FIFO (First-In, First-Out) principle**. Think of a line at a doctor's office or for milk. Elements are added at one end (tail) and removed from the other (front).
*   **Deque** (pronounced "Deck", not "D-Q"): Stands for **Double Ended Queue**. It allows insertions and deletions from **both ends**.
*   **Map**: Stores **key-value pairs**, similar to a dictionary. Each **key is unique**, and it maps to a specific value. Map **does not extend the Collection interface**; it's a separate hierarchy.

### 3. Collection Hierarchy

The complete hierarchy starts with the `Iterable` interface.
*   **Iterable Interface**: This is the **root interface** of the entire Collection hierarchy. It is part of the `java.lang` package.
    *   Any class that implements `Iterable` can have **for-each loops** applied to its objects.
    *   `Collection` extends `Iterable`.
    *   `List`, `Set`, `Queue` all extend `Collection`. This means all objects in the `Collection` hierarchy can be iterated over using a for-each loop.
*   **Collection Interface**:
    *   It is a **root interface** in the `java.util` package.
    *   Child interfaces like `List`, `Set`, `Queue` extend it.
    *   It cannot be **instantiated directly**; it provides a **blueprint** for basic operations (e.g., `size()`, `isEmpty()`, `contains()`, `add()`, `remove()`). Any class implementing `Collection` (or its child interfaces) must implement these methods.

### 4. List Interface and Implementations

The `List` interface, part of `java.util` package, extends `Collection`.
*   **When to use List**:
    *   When an **ordered sequence** is required, meaning elements are stored and retrieved in the order they were put in.
    *   When **duplicate elements are allowed**.
*   **Key Features**:
    *   **Order Preservation**: Maintains the insertion order of elements.
    *   **Index-based Access**: Elements can be accessed using their integer index, similar to arrays.
    *   **Duplicate Elements**: Allows duplicate elements.

#### 4.1. ArrayList

*   **Definition**: An implementation of the `List` interface. Unlike fixed-size arrays, `ArrayList` **dynamically increases its size** as more elements are added.
*   **Creation**:
    ```java
    import java.util.ArrayList;
    import java.util.List;

    // Generics are used to specify the type of elements it will store for type safety
    ArrayList<Integer> arrayList = new ArrayList<>();
    // Since Java 7, you can omit the type on the right side (diamond operator)
    ArrayList<Integer> arrayList2 = new ArrayList<>();
    // Recommended way: use the parent interface for reference
    List<Integer> list = new ArrayList<>(); //
    ```
    *   **Initial Capacity**: By default, an `ArrayList` has an **initial capacity of 10**. This is the size of the internal array that holds the elements. You can specify the initial capacity in the constructor:
        ```java
        List<Integer> listWithCapacity = new ArrayList<>(1000); //
        // Size will still be 0, but capacity is 1000, avoiding resizing overhead for up to 1000 elements.
        ```
    *   **`Arrays.asList()`**: Creates a **fixed-size list** from an array or comma-separated values. **Elements cannot be added or removed**, but they can be replaced.
        ```java
        List<String> fixedList = java.util.Arrays.asList("Monday", "Tuesday"); //
        // fixedList.add("Wednesday"); // Throws UnsupportedOperationException
        fixedList.set(1, "Wednesday"); // Replaces "Tuesday" with "Wednesday"
        ```
        Internally, `Arrays.asList()` returns an instance of a **private static nested class** within `Arrays`, not `java.util.ArrayList`. To make it modifiable, pass it to a new `ArrayList` constructor:
        ```java
        List<String> modifiableList = new ArrayList<>(fixedList); //
        modifiableList.add("Wednesday"); // Works
        ```
    *   **`List.of()` (Java 9+)**: Creates an **unmodifiable list**. **Neither elements can be added/removed nor replaced**.
        ```java
        List<Integer> unmodifiableList = List.of(1, 2, 3); //
        // unmodifiableList.set(1, 33); // Throws UnsupportedOperationException
        ```
*   **Core Methods**:
    *   **`add(E element)`**: Adds an element to the **end** of the list.
        ```java
        list.add(1);
        list.add(5);
        list.add(80); // List:
        ```
    *   **`add(int index, E element)`**: Inserts an element at a **specific index**. Existing elements are shifted to the right.
        ```java
        list.add(1, 50); // List:
        ```
    *   **`get(int index)`**: Retrieves the element at the specified index. **Zero-based indexing**.
        ```java
        int firstItem = list.get(0); // Returns 1
        ```
    *   **`size()`**: Returns the number of elements in the list.
        ```java
        int size = list.size(); // Returns 3 for
        ```
    *   **Looping (Iteration)**:
        *   **For loop (index-based)**:
            ```java
            for (int i = 0; i < list.size(); i++) {
                System.out.println(list.get(i)); //
            }
            ```
        *   **For-each loop**: Iterates directly over elements. Applicable because `ArrayList` implements `Iterable`.
            ```java
            for (int x : list) {
                System.out.println(x); //
            }
            ```
    *   **`contains(Object o)`**: Checks if an element exists in the list. Returns `boolean`.
        ```java
        boolean exists = list.contains(50); // Returns true
        ```
    *   **`remove(int index)`**: Removes the element at the specified index. Elements to the right are shifted left.
        ```java
        list.remove(2); // Removes element at index 2 (80 from)
        ```
    *   **`remove(Object o)`**: Removes the **first occurrence** of the specified element.
        ```java
        List<String> fruits = new ArrayList<>(List.of("Apple", "Banana", "Apple"));
        fruits.remove("Apple"); // Removes the first "Apple"
        // To ensure Object version is called for Integers, use `Integer.valueOf()`
        list.remove(Integer.valueOf(1)); // Removes the object 1, not element at index 1
        ```
    *   **`set(int index, E element)`**: **Replaces** the element at the specified index with a new element.
        ```java
        list.set(2, 50); // Replaces element at index 2 with 50
        ```
    *   **`addAll(Collection<? extends E> c)`**: Adds all elements from another collection to the end of the list.
        ```java
        List<Integer> anotherList = List.of(4, 5, 7, 8, 9);
        list.addAll(anotherList); // Appends elements from anotherList
        ```
    *   **`toArray()`**: Converts the list to an array.
        ```java
        Object[] arr = list.toArray(); // Returns Object[]
        // To specify type, provide a zero-sized array of the desired type
        Integer[] intArray = list.toArray(new Integer); //
        ```
*   **Internal Working (Resizing)**:
    *   `ArrayList` is internally backed by an **array of objects**.
    *   When the internal array is full, `ArrayList` creates a **new, larger array** (typically **1.5 times the current capacity** in Java 8) and **copies all existing elements** from the old array to the new one.
    *   This **copying operation** is the reason why `add` and `remove` operations can have a worst-case time complexity of O(n).
*   **Capacity vs. Size**:
    *   **Capacity**: The actual size of the internal array.
    *   **Size**: The number of elements currently stored in the `ArrayList`.
*   **`trimToSize()`**: Reduces the capacity of the `ArrayList` to its current size, potentially saving memory. `ArrayList` **does not automatically shrink** its size when elements are removed.
    ```java
    // After removing elements, capacity might still be high.
    // list.trimToSize(); //
    ```
    *   (Note: There's no direct method to print `ArrayList` capacity, but it can be accessed using **reflection** for educational purposes.)
*   **Time Complexity**:
    *   **`get(index)`**: **O(1)** (constant time) because it's index-based access in an array.
    *   **`add(element)` / `add(index, element)`**: **O(1)** on average (amortized constant time), but **O(n) in worst case** (when resizing or shifting elements at the beginning).
    *   **`remove(index)` / `remove(Object)`**: **O(n) in worst case** (when removing from the beginning, requiring all subsequent elements to be shifted).
    *   **Looping**: **O(n)** (linear time), as it iterates over all elements.

#### 4.2. Comparator Interface

*   **Definition**: A **functional interface** (`java.util.Comparator`) that enables **custom ordering**. It has a single abstract method: `compare(T o1, T o2)`.
*   **Purpose**: Used when **natural ordering is not desired** or when sorting by **multiple criteria**.
*   **`compare(o1, o2)` Method Logic**:
    *   **Negative integer**: `o1` comes before `o2`.
    *   **Zero**: `o1` and `o2` are considered equal in terms of ordering.
    *   **Positive integer**: `o1` comes after `o2`.
*   **Implementation using Lambda Expressions**:
    ```java
    List<String> words = new ArrayList<>(List.of("Apple", "Date", "Banana"));
    // Natural Order (Ascending)
    words.sort(null); //
    // Or
    words.sort((s1, s2) -> s1.compareTo(s2)); //

    // Custom Order (Descending by length)
    words.sort((s1, s2) -> s2.length() - s1.length()); //
    // List: [Banana, Apple, Date]

    // Sorting custom objects (e.g., Student by GPA)
    class Student {
        String name;
        double gpa;
        // Constructor, getters, toString
    }
    List<Student> students = new ArrayList<>();
    students.add(new Student("Alice", 3.5));
    students.add(new Student("Bob", 3.7));
    students.add(new Student("Charlie", 3.5));

    // Sort by GPA (descending)
    students.sort((s1, s2) -> Double.compare(s2.gpa, s1.gpa)); //

    // Chaining comparators (Java 8+)
    // Sort by GPA (descending), then by Name (ascending) for ties
    students.sort(Comparator.comparingDouble(Student::getGpa).reversed()
                            .thenComparing(Student::getName)); //
    ```
*   **Comparable vs. Comparator**:
    *   **`Comparable`**: An interface (`java.lang.Comparable`) implemented by a class to define its **natural ordering**. It has a single method: `compareTo(T other)`.
        *   Used when `List.sort(null)` is called.
        *   Example: `Integer` and `String` classes implement `Comparable`.
    *   **`Comparator`**: A separate interface used to define **custom sorting logic** (external to the class).

#### 4.3. LinkedList

*   **Definition**: An implementation of the `List` interface that uses a **doubly linked list** structure internally. Elements are stored as **Nodes**, which are not necessarily in **contiguous memory locations**.
*   **Node Structure**: Each `Node` contains two main parts:
    *   **Data**: The actual element stored (e.g., integer, string, object).
    *   **Pointers/References**: A reference to the **next node** and (in a doubly linked list) a reference to the **previous node**.
    ```java
    // Conceptual Node class
    class Node {
        int value;
        Node next; // Pointer to next node
        Node previous; // Pointer to previous node (for doubly linked list)
    }
    ```
*   **Creation**:
    ```java
    import java.util.LinkedList;
    List<Integer> linkedList = new LinkedList<>(); //
    ```
*   **Key Features**:
    *   **Efficient Insertions and Deletions in Middle**: **O(1)** (constant time) because it only requires updating pointers, without shifting elements.
    *   **Slower Random Access**: **O(n)** (linear time) for `get(index)` because it must **traverse the list from the beginning** (or end in a doubly linked list) to reach the desired index.
    *   **More Memory Overhead**: Each node stores data *and* pointers, requiring more memory compared to `ArrayList`.
*   **Methods**: `LinkedList` provides methods for list operations, and also specific methods related to its double-ended nature.
    *   `addFirst(E e)` / `addLast(E e)`: Adds at the beginning/end. (O(1))
    *   `getFirst()` / `getLast()`: Retrieves first/last element. (O(1))
    *   `removeFirst()` / `removeLast()`: Removes first/last element. (O(1))
    *   `removeIf(Predicate<? super E> filter)`: Removes elements based on a condition (Java 8+).
        ```java
        linkedList.removeIf(num -> num % 2 == 0); // Remove even numbers
        ```
    *   `removeAll(Collection<?> c)`: Removes all elements contained in another collection.
*   **Acting as Stack & Queue**:
    *   `LinkedList` can act as a **Stack** (LIFO) using methods like `addFirst()` (push) and `removeFirst()` (pop).
    *   `LinkedList` can act as a **Queue** (FIFO) using methods like `addLast()` (enqueue) and `removeFirst()` (dequeue).
*   **Time Complexity**:
    *   **`add(index, element)` / `remove(index)` at ends**: O(1).
    *   **`add(index, element)` / `remove(index)` in middle**: O(n) (to find the node), then O(1) (to modify pointers).
    *   **`get(index)`**: O(n).

#### 4.4. Vector

*   **Definition**: A **legacy class** (`java.util.Vector`) that implements the `List` interface. It was present even **before the Collection Framework** (JDK 1.0).
*   **Key Feature: Synchronization**: The main difference is that `Vector` is **synchronized** (or **thread-safe**). All its methods are synchronized, meaning **only one thread can access the `Vector` at a time**.
*   **Dynamic Array**: Like `ArrayList`, it's backed by a dynamic array.
*   **Capacity Increment**: By default, `Vector` **doubles its capacity** when full. You can also specify a custom capacity increment in the constructor.
    ```java
    Vector<Integer> vector = new Vector<>(); // Initial capacity 10
    Vector<Integer> vectorWithCapacity = new Vector<>(5); // Capacity 5
    // Capacity 5, increment by 3 when full
    Vector<Integer> vectorWithIncrement = new Vector<>(5, 3); //
    ```
    *   `Vector` also provides a `capacity()` method to check its internal array size, unlike `ArrayList`.
*   **Performance**: Due to synchronization overhead (locking and unlocking), `Vector` is generally **slower than `ArrayList` and `LinkedList` in single-threaded environments**.
*   **Use Case**: Primarily recommended when **thread safety is a concern**.
*   **Thread Safety Demonstration**:
    ```java
    // With ArrayList (not thread-safe), final size is inconsistent/less than 2000
    // With Vector (thread-safe), final size is consistently 2000
    ```

#### 4.5. Stack

*   **Definition**: A legacy class (`java.util.Stack`) that represents a **Last-In, First-Out (LIFO)** stack. Think of a stack of cookies or books where you remove the top one first.
*   **Inheritance**: **Extends `Vector`**. This means it inherits all `Vector`'s methods, including its **synchronization** (making `Stack` thread-safe).
*   **Core Stack Operations**:
    *   **`push(E item)`**: Adds an item to the **top** of the stack.
    *   **`pop()`**: Removes and returns the item at the **top** of the stack.
    *   **`peek()`**: Returns the item at the **top** of the stack **without removing it**.
    *   **`isEmpty()`**: Checks if the stack is empty.
    *   **`size()`**: Returns the number of items in the stack.
    *   **`search(Object o)`**: Returns the 1-based position of the object from the top of the stack (-1 if not found).
*   **Example**:
    ```java
    import java.util.Stack;
    Stack<Integer> stack = new Stack<>();
    stack.push(1);
    stack.push(2);
    stack.push(3); // Stack: (3 is top)
    System.out.println(stack.pop()); // Prints 3, Stack:
    System.out.println(stack.peek()); // Prints 2, Stack:
    System.out.println(stack.search(1)); // Prints 2 (1-based index from top)
    ```
*   **Synchronization Overhead**: Being synchronized, `Stack` also incurs performance overhead, similar to `Vector`.
*   **Alternative Implementations**:
    *   `LinkedList` can be used as a stack (recommended over `java.util.Stack`) using `addFirst()`/`push()` and `removeFirst()`/`pop()`.
    *   `ArrayDeque` is another recommended option for stack implementation.
    *   `ArrayList` *can* be used as a stack (using `add()` for push, `get(size-1)` for peek, `remove(size-1)` for pop), but it's **not good practice** as it doesn't provide dedicated methods for stack operations.

#### 4.6. CopyOnWriteArrayList

*   **Purpose**: A **thread-safe** alternative to `ArrayList` and `LinkedList` for scenarios where **reads vastly outnumber writes**. It avoids `ConcurrentModificationException` during iteration while modification occurs.
*   **"Copy on Write" Mechanism**:
    *   **Read operations**: Are **fast and direct**.
    *   **Write operations** (add, remove, set): Instead of modifying the existing list, a **new copy of the internal array is created**, the modification is made on the new copy, and then the original list's reference is updated to point to the new copy.
    *   This ensures that **threads currently reading the original list are unaffected** and see a consistent snapshot of the data. Future reads will see the updated list.
*   **Behavior during Iteration**: When iterating, the `Iterator` operates on a **stable snapshot** of the list. Any modifications made during iteration will **not be reflected** in the ongoing iteration (they apply to a new copy). The updated list will only be seen by new iterators or after the current iteration completes and the reference is updated.
*   **Memory Consumption**: Can be **memory intensive** if there are frequent write operations, as each write creates a new copy of the entire underlying array.
*   **Use Cases**: Ideal for **read-heavy environments** like managing listeners or configuration lists where consistency during iteration is crucial, and writes are infrequent.
*   **Example**:
    ```java
    import java.util.ArrayList;
    import java.util.concurrent.CopyOnWriteArrayList;

    List<String> shoppingList = new ArrayList<>(List.of("Milk", "Eggs", "Bread"));
    // This will throw ConcurrentModificationException
    // for (String item : shoppingList) {
    //     if (item.equals("Eggs")) {
    //         shoppingList.add("Butter"); // Modifying while iterating
    //     }
    // }

    CopyOnWriteArrayList<String> safeShoppingList = new CopyOnWriteArrayList<>(List.of("Milk", "Eggs", "Bread"));
    // This will not throw an exception
    for (String item : safeShoppingList) {
        if (item.equals("Eggs")) {
            safeShoppingList.add("Butter"); // Modifies a new copy
        }
    }
    // The "Butter" will only appear after the loop completes for new operations or printouts
    System.out.println(safeShoppingList); // Will show "Milk", "Eggs", "Bread", "Butter"
    ```

### 5. Map Interface and Implementations

The `Map` interface represents a mapping from keys to values.
*   **Key Characteristics**:
    *   **Key-Value Pairs**: Each entry in a map consists of a unique key and its associated value.
    *   **Unique Keys**: Keys must be unique; a map cannot contain duplicate keys. If you `put` a value with an existing key, the **old value is replaced**.
    *   **One Value per Key**: Each key maps to exactly one value.
    *   **No Extension from Collection**: `Map` is a separate hierarchy and does not extend the `Collection` interface.

#### 5.1. HashMap

*   **Definition**: A hash table-based implementation of the `Map` interface. It **does not guarantee any order** of its elements.
*   **Key Characteristics**:
    *   **No Order**: Elements are not stored or retrieved in any specific order (neither insertion nor sorted).
    *   **Nulls Allowed**: Allows **one null key** and **multiple null values**.
    *   **Not Synchronized**: It is **not thread-safe**.
*   **Creation**:
    ```java
    import java.util.HashMap;
    import java.util.Map;

    Map<Integer, String> studentMap = new HashMap<>(); //
    ```
*   **Core Methods**:
    *   **`put(K key, V value)`**: Inserts a key-value pair. If the key already exists, its value is replaced.
        ```java
        studentMap.put(1, "Akshit");
        studentMap.put(2, "Neha");
        studentMap.put(3, "Shubham"); //
        studentMap.put(2, "Mehul"); // Replaces Neha with Mehul for key 2
        ```
    *   **`get(Object key)`**: Retrieves the value associated with the specified key. Returns `null` if the key is not found.
        ```java
        String studentName = studentMap.get(3); // Returns "Shubham"
        String notFound = studentMap.get(69); // Returns null
        ```
    *   **`containsKey(Object key)`**: Checks if the map contains the specified key.
    *   **`containsValue(Object value)`**: Checks if the map contains the specified value.
    *   **`keySet()`**: Returns a `Set` view of the keys contained in this map. Useful for iterating over keys.
        ```java
        for (Integer rollNum : studentMap.keySet()) {
            System.out.println(studentMap.get(rollNum)); // Prints values based on keys
        }
        ```
    *   **`entrySet()`**: Returns a `Set` view of the mappings (key-value pairs) contained in this map.
        ```java
        for (Map.Entry<Integer, String> entry : studentMap.entrySet()) {
            System.out.println(entry.getKey() + " = " + entry.getValue()); //
            entry.setValue(entry.getValue().toUpperCase()); // Modifying value via entry
        }
        ```
    *   **`remove(Object key)`**: Removes the mapping for a specified key.
    *   **`remove(Object key, Object value)`**: Removes the mapping only if the key maps to the specified value.
    *   **`getOrDefault(Object key, V defaultValue)` (Java 8+)**: Returns the value for the specified key, or a default value if the key is not found.
    *   **`putIfAbsent(K key, V value)` (Java 8+)**: Inserts the specified key-value pair only if the key is not already mapped to a value.
*   **Time Complexity**:
    *   **`put` / `get` / `remove` / `containsKey`**: **O(1) on average** (constant time) due to direct bucket access via hashing.
    *   **Worst case for `put`/`get`/`remove`**: **O(log n)** (after Java 8 treeification) or **O(n)** (if many collisions result in a long linked list before Java 8).
    *   **`containsValue`**: **O(n)** (linear time) because it may need to iterate over all entries.
    *   **`size`**: **O(1)** as it's stored in a separate field.

#### 5.1.1. Internal Structure of HashMap

`HashMap` internally uses an **array** (called **buckets** or **table**) to store key-value pairs.
*   **Four Basic Components**:
    1.  **Key**: The unique identifier for an entry.
    2.  **Value**: The data associated with the key.
    3.  **Bucket/Array**: The internal array where key-value pairs are stored.
    4.  **Hash Function**: An algorithm that takes a key as input and returns a **fixed-size numerical value (hash code)**.
*   **How Data is Stored (`put` operation)**:
    1.  **Hash the Key**: The key is passed to a **hash function** (usually `hashCode()` of the key object) to generate a hash code.
    2.  **Find Index/Bucket**: The hash code is then used with the formula `hash code % array size` to determine the **index (bucket)** in the internal array where the key-value pair will be stored.
    3.  **Store in Bucket**: The key-value pair is stored at the calculated index in the bucket.
*   **Collision Handling**:
    *   A **collision** occurs when two **different keys** produce the **same hash code** (and thus the same array index).
    *   **Java's HashMap handles collisions using**:
        *   **Linked Lists (before Java 8 and for small collision chains)**: If a collision occurs, the new key-value pair is added to a **linked list** at that bucket's index. Each bucket essentially holds a linked list of entries that map to the same hash bucket.
        *   **Balanced Trees (Red-Black Trees, Java 8 and later)**: If the number of entries in a single bucket's linked list **exceeds a certain threshold (default 8)**, the linked list is converted into a **Red-Black Tree** to improve search performance from O(n) to O(log n). This is called **treeification**.
*   **How Data is Retrieved (`get` operation)**:
    1.  **Hash the Key**: The key's hash code is generated using the same hash function used during insertion.
    2.  **Find Index**: The hash code is used to determine the correct bucket index.
    3.  **Find Key in Bucket**: Once the correct bucket (array index) is found, the **linked list or Red-Black Tree** at that index is traversed to find the specific key. **Equality is checked using the `equals()` method** of the key object.
*   **Rehashing**:
    *   When the number of entries in the `HashMap` **exceeds a certain threshold**, the internal array is **resized** to a larger capacity (typically double). This threshold is determined by `capacity * load factor` (default load factor is **0.75**).
    *   During rehashing, all existing entries are re-hashed and redistributed into the new, larger array, as their bucket index calculations will change with the new array size.

#### 5.1.2. `hashCode()` and `equals()` Methods

*   These two methods are crucial for custom objects when used as **keys in `HashMap`** (and `HashSet`).
*   **Default Behavior (from `Object` class)**:
    *   `hashCode()`: Generates a hash code based on the **memory address** of the object. So, every new instance, even if logically identical, will have a different hash code.
    *   `equals()`: Checks for **reference equality** (whether two references point to the exact same object in memory).
*   **Problem with Default Behavior**: If you use custom objects as keys without overriding `hashCode()` and `equals()`, `HashMap` might store logically identical objects as separate entries or fail to retrieve existing ones, because it compares them by memory address instead of their content.
*   **Overriding for Custom Objects**: When overriding, you must ensure:
    1.  If two objects are **equal according to `equals()`**, then they **must have the same `hashCode()`**.
    2.  If two objects have the **same `hashCode()`**, they **are not necessarily equal** (this is a collision, handled by traversing the bucket's linked list/tree and then using `equals()`).
    *   **Example (Person class with `name` and `id`)**:
        ```java
        class Person {
            private String name;
            private int id;

            public Person(String name, int id) {
                this.name = name;
                this.id = id;
            }

            // Getters...

            @Override
            public boolean equals(Object o) {
                if (this == o) return true;
                if (o == null || getClass() != o.getClass()) return false;
                Person person = (Person) o;
                return id == person.id && Objects.equals(name, person.name); //
            }

            @Override
            public int hashCode() {
                return Objects.hash(name, id); //
            }
        }
        ```
    *   **Demonstration**:
        ```java
        Map<Person, String> map = new HashMap<>();
        Person p1 = new Person("Alice", 1);
        Person p2 = new Person("Bob", 2);
        Person p3 = new Person("Alice", 1); // Logically same as p1

        map.put(p1, "Engineer");
        map.put(p2, "Designer");
        map.put(p3, "Manager"); // With overridden hashCode/equals, this will replace p1's value

        System.out.println("Map size: " + map.size()); // Prints 2 (p1 and p3 are merged)
        System.out.println("P1's designation: " + map.get(p1)); // Prints "Manager"
        ```

#### 5.2. LinkedHashMap

*   **Definition**: An implementation of the `Map` interface that **maintains insertion order** of key-value pairs. It combines the features of `HashMap` and `LinkedList`.
*   **Internal Working**: It extends `HashMap` and uses a **doubly linked list** to connect all its entries in the order they were inserted.
*   **Key Characteristics**:
    *   **Order Maintained**: Preserves the order in which elements were inserted.
    *   **Slightly Slower**: Due to the overhead of maintaining the linked list, it can be slightly slower than `HashMap` for `put` and `get` operations.
    *   **More Memory**: Consumes slightly more memory than `HashMap` due to the linked list pointers.
*   **`accessOrder` (Constructor parameter)**:
    *   `false` (default): Entries are ordered by **insertion order**.
    *   `true`: Entries are ordered by **access order** (elements move to the end of the linked list on access, useful for **LRU (Least Recently Used) Caches**).
        ```java
        import java.util.LinkedHashMap;
        Map<String, Integer> linkedMap = new LinkedHashMap<>(16, 0.75f, true); // Access order true
        linkedMap.put("Orange", 80);
        linkedMap.put("Apple", 10);
        linkedMap.put("Guava", 20); // Insertion order: Orange, Apple, Guava

        System.out.println(linkedMap); // Prints: {Orange=80, Apple=10, Guava=20}
        linkedMap.get("Orange"); // Accesses Orange
        System.out.println(linkedMap); // With accessOrder=true, Orange moves to end: {Apple=10, Guava=20, Orange=80}
        ```
*   **LRU Cache Example**: A common use case for `LinkedHashMap` with `accessOrder=true` is implementing an LRU cache. You can subclass `LinkedHashMap` and override `removeEldestEntry()` to define when to remove the least recently used entry when capacity is exceeded.

#### 5.3. WeakHashMap

*   **Definition**: A `HashMap` implementation where the **keys are stored as weak references**.
*   **Weak References and Garbage Collection**:
    *   A **strong reference** (e.g., `Phone phone = new Phone();`) prevents the referenced object from being garbage collected.
    *   A **weak reference** does not prevent garbage collection. If an object is only reachable via weak references, it becomes eligible for garbage collection.
    *   The **Garbage Collector (GC)** automatically reclaims memory occupied by objects that are no longer strongly reachable. You can suggest GC to JVM using `System.gc()`, but it's ultimately up to the JVM.
*   **Key Behavior**:
    *   If a key in `WeakHashMap` is **no longer strongly referenced** elsewhere, it becomes eligible for garbage collection.
    *   When the key is garbage collected, its corresponding **entry (key-value pair) is automatically removed** from the `WeakHashMap`.
*   **Use Case**: Ideal for **caching** scenarios where keys are temporary and you don't want the cache to prevent objects from being garbage collected if they are no longer in ordinary use.
*   **Caveat with String Literals**: String literals (`"Image One"`) are stored in the String Pool and are **strongly referenced throughout the program's lifecycle**. Using them as keys in `WeakHashMap` will prevent them from being garbage collected, defeating the purpose. To demonstrate weak reference behavior, use `new String("Image One")` for keys to create distinct objects not in the pool.
    ```java
    import java.util.WeakHashMap;
    // Assume Image class with name and toString()
    WeakHashMap<Object, String> imageCache = new WeakHashMap<>();

    // Using non-literal String objects as keys
    String key1 = new String("ImageOne"); // Not from String Pool
    String key2 = new String("ImageTwo");

    imageCache.put(key1, "Value for ImageOne");
    imageCache.put(key2, "Value for ImageTwo");
    System.out.println("Cache before GC: " + imageCache); // Prints all entries

    key1 = null; // No more strong reference to "ImageOne" object
    key2 = null; // No more strong reference to "ImageTwo" object

    System.gc(); // Suggest Garbage Collection (JVM's discretion)
    try { Thread.sleep(100); } catch (InterruptedException e) {} // Wait for GC

    System.out.println("Cache after GC: " + imageCache); // May print empty or some entries
    // If keys were String literals ("ImageOne"), they would not be GCed
    ```

#### 5.4. IdentityHashMap

*   **Definition**: An implementation of the `Map` interface that uses **reference equality (`==`)** instead of object equality (`equals()`) for comparing keys and values.
*   **Key Characteristics**:
    *   **Reference Equality**: Compares keys and values using `==`. This means two keys are considered equal only if they are the **exact same object in memory**.
    *   **Uses `Object.hashCode()`**: It relies on the default `hashCode()` method provided by the `Object` class (which is based on memory address), even if the key class overrides `hashCode()`.
*   **Differences from `HashMap`**:
    *   `HashMap` uses `equals()` and `hashCode()` (overridden methods if available) to determine equality and hash codes.
    *   `IdentityHashMap` uses `==` and `Object.hashCode()` for all comparisons.
*   **Use Case**: Primarily used for **topology-preserving object graph transformations** or when you need a map that distinguishes between two objects that are `equals()` but are distinct objects in memory.
    ```java
    import java.util.HashMap;
    import java.util.IdentityHashMap;
    import java.util.Map;

    String key1 = new String("key"); // Creates a new String object in heap
    String key2 = new String("key"); // Creates another new String object in heap

    // HashMap will treat key1 and key2 as the same because their content is equal()
    Map<String, String> hashMap = new HashMap<>();
    hashMap.put(key1, "Value1");
    hashMap.put(key2, "Value2");
    System.out.println("HashMap: " + hashMap); // Prints {key=Value2} (key1's value is replaced)

    // IdentityHashMap will treat key1 and key2 as different because they are distinct objects (not ==)
    Map<String, String> identityHashMap = new IdentityHashMap<>();
    identityHashMap.put(key1, "Value1");
    identityHashMap.put(key2, "Value2");
    System.out.println("IdentityHashMap: " + identityHashMap); // Prints {key=Value1, key=Value2}
    ```

#### 5.5. SortedMap Interface

*   **Definition**: An interface that extends `Map` and **guarantees that its entries are sorted by the keys**.
*   **Sorting Order**: Can be either:
    *   **Natural ordering**: If keys implement the `Comparable` interface.
    *   **Custom order**: By providing a `Comparator` during creation.
*   **Implementation**: The primary implementation of `SortedMap` is **`TreeMap`**.
*   **Key Methods (beyond `Map` interface)**:
    *   `firstKey()`: Returns the lowest key currently in the map.
    *   `lastKey()`: Returns the highest key currently in the map.
    *   `headMap(K toKey)`: Returns a view of the portion of this map whose keys are strictly less than `toKey`.
    *   `tailMap(K fromKey)`: Returns a view of the portion of this map whose keys are greater than or equal to `fromKey`.
    *   `subMap(K fromKey, K toKey)`: Returns a view of the portion of this map whose keys range from `fromKey` (inclusive) to `toKey` (exclusive).

#### 5.6. TreeMap

*   **Definition**: A **Red-Black Tree** based implementation of the `SortedMap` and `NavigableMap` interfaces.
*   **Internal Implementation**: Uses a **Red-Black Tree**, which is a **self-balancing binary search tree**. This ensures that the tree remains balanced after insertions and deletions, guaranteeing logarithmic time complexity for most operations.
*   **Sorting**: Stores entries in **ascending order of keys** by default (natural ordering) or according to a specified `Comparator`.
*   **Time Complexity**:
    *   **`put` / `get` / `remove` / `containsKey`**: **O(log n)** (logarithmic time) due to the balanced tree structure.
    *   **`containsValue`**: **O(n)** (linear time) as it requires traversing the entire tree.
*   **Example**:
    ```java
    import java.util.TreeMap;
    import java.util.Comparator; // For custom sorting

    TreeMap<Integer, String> studentMap = new TreeMap<>();
    studentMap.put(91, "Vivek");
    studentMap.put(99, "Shubham");
    studentMap.put(78, "Mohit");
    studentMap.put(77, "Vipul");
    System.out.println(studentMap); // Prints in key order: {77=Vipul, 78=Mohit, 91=Vivek, 99=Shubham}

    // Custom sorting (descending order of keys)
    TreeMap<Integer, String> descStudentMap = new TreeMap<>(Comparator.reverseOrder()); //
    descStudentMap.put(91, "Vivek");
    descStudentMap.put(99, "Shubham");
    descStudentMap.put(78, "Mohit");
    System.out.println(descStudentMap); // Prints: {99=Shubham, 91=Vivek, 78=Mohit}
    ```

#### 5.7. NavigableMap Interface

*   **Definition**: An interface that extends `SortedMap` and provides **navigation methods** to find elements that are closest matches to a given key, or to retrieve sub-maps or maps in reverse order.
*   **Implementation**: `TreeMap` also implements `NavigableMap`.
*   **Key Methods**:
    *   `lowerKey(K key)`: Returns the greatest key strictly less than the given key.
    *   `floorKey(K key)`: Returns the greatest key less than or equal to the given key.
    *   `ceilingKey(K key)`: Returns the least key greater than or equal to the given key.
    *   `higherKey(K key)`: Returns the least key strictly greater than the given key.
    *   `firstEntry()`, `lastEntry()`: Return `Map.Entry` objects for first/last elements.
    *   `pollFirstEntry()`, `pollLastEntry()`: Remove and return first/last entries.
    *   `descendingMap()`: Returns a reverse order view of the map.
    ```java
    import java.util.NavigableMap;
    NavigableMap<Integer, String> navMap = new TreeMap<>();
    navMap.put(1, "One");
    navMap.put(3, "Three");
    navMap.put(5, "Five");
    System.out.println(navMap.lowerKey(4)); // Prints 3
    System.out.println(navMap.ceilingKey(4)); // Prints 5
    System.out.println(navMap.higherEntry(1)); // Prints 3=Three
    System.out.println(navMap.descendingMap()); // Prints {5=Five, 3=Three, 1=One}
    ```

#### 5.8. Hashtable

*   **Definition**: A **legacy** (JDK 1.0) hash table implementation that implements the `Map` interface.
*   **Key Characteristics**:
    *   **Synchronized**: All its methods are **synchronized**, making it **thread-safe**.
    *   **No Nulls**: **Does not allow null keys or null values**.
    *   **Performance**: Generally **slower than `HashMap`** due to the overhead of synchronization (even for read operations, the entire table is locked).
    *   **Collision Handling**: Uses **only linked lists** for collision resolution; it does **not use Red-Black trees** like `HashMap` (Java 8+).
*   **Use Case**: Modern applications generally prefer `ConcurrentHashMap` for thread-safe map operations due to its better performance.
    ```java
    import java.util.Hashtable;
    import java.util.Map;

    Hashtable<Integer, String> hashtable = new Hashtable<>(); //
    hashtable.put(1, "Apple");
    hashtable.put(2, "Banana");
    // hashtable.put(3, null); // Throws NullPointerException
    // hashtable.put(null, "Guava"); // Throws NullPointerException

    // Demonstrating thread safety vs HashMap
    // HashMap would lead to inconsistent size when multiple threads write
    // Hashtable ensures consistent size (2000 for 1000+1000 writes) due to synchronization
    ```

#### 5.9. ConcurrentHashMap

*   **Purpose**: A **thread-safe** and **highly concurrent** implementation of the `Map` interface. It offers much **better performance than `Hashtable`** for concurrent access.
*   **Internal Implementation**:
    *   **Java 7 (Segment-based locking)**: The map was divided into **segments** (default 16 small `HashMaps`), each with its own independent lock. This allowed multiple threads to operate on different segments concurrently.
    *   **Java 8+ (Compare-And-Swap / CAS)**: The segmentation concept was removed. `ConcurrentHashMap` now uses **lock-free algorithms (Compare-And-Swap or CAS)** for most operations.
        *   **CAS (Compare-And-Swap)**: An atomic operation that attempts to update a value only if it's currently at an expected value. If the expected value doesn't match the current value (meaning another thread modified it), the operation fails, and the thread can retry. This **avoids explicit locking** for most read and write operations, improving concurrency.
        *   **Locking only for specific scenarios**: Locks are still used for complex operations like **rehashing** (resizing the internal array) and for handling **collision chains** that become trees.
*   **Time Complexity**: **O(1) on average** for `put`, `get`, `remove`, `containsKey`.
*   **Rehashing**: Uses **incremental rehashing** where only portions of the table are resized at a time, allowing other threads to continue operating on unaffected parts.
*   **Key Features**:
    *   **High Concurrency**: Multiple threads can perform read and write operations simultaneously with minimal blocking.
    *   **No Nulls**: Does **not allow null keys or null values** (similar to `Hashtable`).
*   **Use Case**: The **recommended choice for thread-safe map operations** in modern Java applications.
    ```java
    import java.util.concurrent.ConcurrentHashMap;
    Map<String, Integer> concurrentMap = new ConcurrentHashMap<>(); //
    // This map can be safely accessed and modified by multiple threads simultaneously.
    ```

#### 5.10. ConcurrentSkipListMap

*   **Purpose**: A **thread-safe** and **sorted** implementation of the `NavigableMap` interface. It is essentially a **thread-safe version of `TreeMap`**.
*   **Internal Implementation**: Uses a **Skip List** data structure.
    *   **Skip List**: A **probabilistic data structure** that combines features of sorted linked lists with multiple "express lanes" or levels. This allows for **efficient O(log n)** average time complexity for search, insertion, and deletion, similar to balanced trees.
    *   **Advantages over Red-Black Trees for Concurrency**: Skip lists are often simpler to implement concurrently than complex tree structures like Red-Black Trees, as they require less complex rebalancing operations during concurrent modifications.
*   **Key Features**:
    *   **Thread-Safe**: Designed for high concurrency.
    *   **Sorted**: Maintains elements in sorted order of keys (natural ordering or `Comparator`).
    *   **NavigableMap Features**: Provides all the navigation methods of `NavigableMap` (e.g., `lowerKey`, `ceilingKey`, `descendingMap`).
*   **Time Complexity**: **O(log n) on average** for `put`, `get`, `remove`, `containsKey`.
*   **Use Case**: When you need a map that is both **thread-safe AND keeps its elements sorted by keys**, for example, in concurrent priority queues or range queries.
    ```java
    import java.util.concurrent.ConcurrentSkipListMap;
    NavigableMap<String, Integer> sortedConcurrentMap = new ConcurrentSkipListMap<>(); //
    sortedConcurrentMap.put("Apple", 1);
    sortedConcurrentMap.put("Orange", 3);
    sortedConcurrentMap.put("Banana", 2);
    System.out.println(sortedConcurrentMap); // Prints: {Apple=1, Banana=2, Orange=3} (sorted by key)
    ```

#### 5.11. EnumMap

*   **Definition**: A specialized `Map` implementation optimized for **enum keys**.
*   **Key Characteristics**:
    *   **Enum Keys**: Keys *must* be of a single `enum` type.
    *   **High Performance**: Extremely **efficient and fast** because it uses an internal array (instead of a hash table) where the `enum` ordinal (index) maps directly to array indices. This avoids hashing and collision overhead.
    *   **Memory Efficient**: Uses less memory than `HashMap`.
    *   **Order Maintained**: Preserves the **natural order of the enum constants** (the order in which they are declared in the enum definition).
    *   **No Nulls**: Does **not allow null keys**.
    *   **Not Synchronized**: It is **not thread-safe**.
*   **Use Case**: Highly recommended whenever you need a `Map` whose keys are instances of an `enum` type.
    ```java
    import java.util.EnumMap;
    import java.util.Map;

    enum Day {
        MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY
    }

    Map<Day, String> schedule = new EnumMap<>(Day.class); //
    schedule.put(Day.TUESDAY, "Gym");
    schedule.put(Day.MONDAY, "Walk");
    System.out.println(schedule); // Prints: {MONDAY=Walk, TUESDAY=Gym} (order of enum declaration)
    ```

#### 5.12. Immutable Maps

*   **Purpose**: To create `Map` instances whose **contents cannot be changed** after creation. This provides **thread safety** and **data integrity**.
*   **Ways to Create**:
    *   **`Collections.unmodifiableMap()`**: Wraps an existing `Map` (e.g., `HashMap`) to create an unmodifiable view.
        *   **Downside**: If the original underlying map is modified, the unmodifiable view will also reflect those changes, which can lead to unexpected behavior.
        ```java
        import java.util.Collections;
        Map<String, Integer> modifiableMap = new HashMap<>();
        modifiableMap.put("A", 1);
        Map<String, Integer> unmodMap = Collections.unmodifiableMap(modifiableMap); //
        // unmodMap.put("B", 2); // Throws UnsupportedOperationException
        modifiableMap.put("C", 3); // Modifies original map
        System.out.println(unmodMap); // Prints {A=1, C=3} - reflects change from original
        ```
    *   **`Map.of()` (Java 9+)**: Provides a **cleaner and safer way** to create **immutable `Map`s directly**.
        *   **Limitations**: `Map.of()` and its overloaded versions are limited to a **maximum of 10 key-value pairs**.
        ```java
        Map<String, Integer> immutableMap = Map.of("Shubham", 90, "Vivek", 89); //
        // immutableMap.put("Akshit", 88); // Throws UnsupportedOperationException
        ```
    *   **`Map.ofEntries()` (Java 9+)**: Allows creating immutable maps with **more than 10 entries** by passing `Map.Entry` objects.
        ```java
        Map<String, Integer> largeImmutableMap = Map.ofEntries(
            Map.entry("Akshit", 99),
            Map.entry("Vivek", 99)
            // ... add more entries than 10 using Map.entry()
        ); //
        ```

### 6. Set Interface and Implementations

The `Set` interface, part of `java.util`, extends `Collection`.
*   **Key Characteristic**: A collection that **does not contain duplicate elements**.

#### 6.1. HashSet

*   **Definition**: A hash table-based implementation of the `Set` interface. It **does not guarantee any order**.
*   **Internal Implementation**: `HashSet` is internally backed by a `HashMap`. Each element added to the `HashSet` is stored as a **key in the internal `HashMap`**, and a **dummy value** (a static object) is used for the corresponding value.
*   **Key Characteristics**:
    *   **No Duplicates**: Automatically handles duplicate elements (only one instance of a value can be in the set).
    *   **No Order**: Elements are not stored in any particular order.
    *   **Nulls Allowed**: Allows one null element.
    *   **Not Synchronized**: Not thread-safe.
*   **Methods**: Similar to `ArrayList` but without index-based access. `add`, `contains`, `remove`, `clear`, `isEmpty`, `size`.
    ```java
    import java.util.HashSet;
    Set<Integer> hashSet = new HashSet<>();
    hashSet.add(12);
    hashSet.add(1);
    hashSet.add(1); // Duplicate, only 1 is stored
    hashSet.add(67);
    System.out.println(hashSet); // Prints in no particular order: (example output)
    ```

#### 6.2. LinkedHashSet

*   **Definition**: An implementation of the `Set` interface that **maintains insertion order**.
*   **Internal Implementation**: It combines `HashSet` (for unique elements) with a **doubly linked list** (for maintaining order).

#### 6.3. TreeSet

*   **Definition**: A **Red-Black Tree** based implementation of the `NavigableSet` interface.
*   **Sorting**: Stores elements in **natural ascending order** or according to a `Comparator` provided at creation.
*   **Key Features**:
    *   **Sorted**: Elements are always stored in sorted order.
    *   **NavigableSet Features**: Provides navigation methods like `lower`, `floor`, `ceiling`, `higher`, `first`, `last`, `pollFirst`, `pollLast`, `descendingSet` (similar to `NavigableMap`).
*   **Time Complexity**: O(log n) for `add`, `contains`, `remove` (similar to `TreeMap`).
    ```java
    import java.util.TreeSet;
    Set<Integer> treeSet = new TreeSet<>();
    treeSet.add(12);
    treeSet.add(1);
    treeSet.add(67);
    System.out.println(treeSet); // Prints: (sorted)
    ```

#### 6.4. EnumSet

*   **Definition**: A specialized `Set` implementation optimized for **enum keys**.
*   **Key Characteristics**: Similar to `EnumMap` in its efficiency and internal array-based implementation, but for sets of enum values.

#### 6.5. Synchronization in Sets

*   **`Collections.synchronizedSet()`**: Wraps an existing `Set` to make it synchronized.
    *   **External Synchronization**: It provides external synchronization, meaning every method call to the wrapped set is put inside a `synchronized` block.
    *   **Performance Overhead**: This can lead to significant performance overhead, especially for read operations, as the entire set is locked during any operation. **Not recommended for high-concurrency scenarios**.
    ```java
    import java.util.Collections;
    Set<Integer> mySet = new HashSet<>();
    Set<Integer> syncSet = Collections.synchronizedSet(mySet); //
    // Iterating over synchronized sets requires manual synchronization:
    // synchronized (syncSet) { //
    //   for (Integer num : syncSet) { ... }
    // }
    ```
*   **`ConcurrentSkipListSet`**:
    *   **Definition**: A **thread-safe** and **sorted** implementation of `NavigableSet`. It's the **concurrent version of `TreeSet`**.
    *   **Internal Implementation**: Uses a **Skip List** (similar to `ConcurrentSkipListMap`).
    *   **Recommended**: It's the **recommended choice for thread-safe sets that need to be sorted**.
    ```java
    import java.util.concurrent.ConcurrentSkipListSet;
    Set<Integer> concurrentSortedSet = new ConcurrentSkipListSet<>(); //
    ```

#### 6.6. Immutable Sets

*   Similar to immutable maps, `Set` provides ways to create unmodifiable sets.
    *   **`Set.of()` (Java 9+)**: Creates an **immutable set** directly. Unlike `Map.of()`, `Set.of()` **does not have a limit of 10 elements**.
    ```java
    Set<Integer> immutableSet = Set.of(1, 2, 3); //
    // immutableSet.add(4); // Throws UnsupportedOperationException
    ```
    *   **`Collections.unmodifiableSet()`**: Wraps an existing `Set` to provide an unmodifiable view. (Same downsides as `Collections.unmodifiableMap()`).

#### 6.7. CopyOnWriteArraySet

*   **Definition**: A **thread-safe** implementation of the `Set` interface using the **"copy-on-write" mechanism**.
*   **Key Characteristics**:
    *   **Thread-Safe**: Ensures consistency in multi-threaded environments.
    *   **Copy-on-Write**: Like `CopyOnWriteArrayList`, all **mutating operations (add, remove)** create a **new copy** of the underlying array, ensuring readers operate on a consistent snapshot.
    *   **No Duplicates**: Inherits the Set property of not allowing duplicate elements.
    *   **Not Sorted**: Elements are not maintained in any specific order.
*   **Use Cases**:
    *   **Read-heavy scenarios with infrequent writes**: When reads significantly outnumber writes, and a consistent snapshot during iteration is required.
    *   **When order is not important and sorting overhead of `ConcurrentSkipListSet` is not desired**.
*   **Behavior during Iteration**: Iterators provide a **snapshot of the array at the time the iterator was created**. Subsequent modifications to the set will not be reflected in the ongoing iteration.
*   **Comparison with `ConcurrentSkipListSet`**:
    *   `CopyOnWriteArraySet` uses an internal array and is unsorted.
    *   `ConcurrentSkipListSet` uses a Skip List and is sorted.
    *   Choose `CopyOnWriteArraySet` for **unsorted, read-heavy scenarios** where consistent iterators are critical.
    *   Choose `ConcurrentSkipListSet` for **sorted, thread-safe scenarios** or when **frequent writes** would make `CopyOnWriteArraySet` inefficient due to constant copying.
    ```java
    import java.util.concurrent.CopyOnWriteArraySet;
    Set<Integer> cowSet = new CopyOnWriteArraySet<>();
    cowSet.add(1); cowSet.add(2); cowSet.add(3); cowSet.add(4); cowSet.add(5);
    // Iterate and modify (will not throw ConcurrentModificationException)
    for (Integer num : cowSet) {
        if (num == 5) {
            cowSet.add(6); // Add is on a new copy
        }
        System.out.print(num + " "); // Prints 1 2 3 4 5
    }
    System.out.println("\nAfter loop: " + cowSet); // Prints 1 2 3 4 5 6
    ```

### 7. Queue Interface and Implementations

The `Queue` interface, part of `java.util`, follows the **FIFO (First-In, First-Out) principle**.
*   **Core Characteristics**:
    *   Elements are **added at one end (the "tail" or "end")**. This operation is called **enqueue**.
    *   Elements are **removed from the other end (the "front" or "head")**. This operation is called **dequeue**.
*   **Core Operations & Methods**:
    *   **Adding Elements**:
        *   `add(E e)`: Inserts element. Throws `IllegalStateException` if the queue is full.
        *   `offer(E e)`: Inserts element. Returns `true` on success, `false` if the queue is full (doesn't throw exception). **Generally preferred for bounded queues**.
    *   **Retrieving and Removing Elements**:
        *   `remove()`: Retrieves and removes the head of the queue. Throws `NoSuchElementException` if the queue is empty.
        *   `poll()`: Retrieves and removes the head of the queue. Returns `null` if the queue is empty (doesn't throw exception). **Generally preferred for empty queue handling**.
    *   **Retrieving Elements (without removal)**:
        *   `element()`: Retrieves, but does not remove, the head of the queue. Throws `NoSuchElementException` if the queue is empty.
        *   `peek()`: Retrieves, but does not remove, the head of the queue. Returns `null` if the queue is empty (doesn't throw exception). **Generally preferred for empty queue handling**.

#### 7.1. LinkedList (as Queue)

*   As seen previously, `LinkedList` can efficiently act as a `Queue` due to its `addLast()` (enqueue) and `removeFirst()` (dequeue) methods, which are O(1).
    ```java
    import java.util.LinkedList;
    import java.util.Queue;
    Queue<Integer> q = new LinkedList<>(); //
    q.add(1); q.add(2); q.add(3); // Enqueue
    System.out.println(q); // Prints
    System.out.println(q.remove()); // Dequeue - prints 1
    System.out.println(q.peek()); // Peek - prints 2
    ```

#### 7.2. PriorityQueue

*   **Definition**: An unbounded queue that orders its elements according to their **natural order** (if they implement `Comparable`) or by a `Comparator` provided at construction time.
*   **Priority Principle**: The element at the head of the queue is always the one with the **highest priority** (smallest value for natural ordering).
*   **Internal Implementation**: `PriorityQueue` is implemented using a **Min-Heap** (a binary heap).
    *   In a Min-Heap, the value of each node is **less than or equal to the values of its children**. This property ensures that the **smallest element is always at the root** (head).
*   **Key Characteristics**:
    *   **No Nulls**: Does not allow null elements.
    *   **Not Internally Sorted**: The `PriorityQueue` itself is **not sorted**. Only the **head element is guaranteed to be the highest priority**. When you iterate over a `PriorityQueue`, elements are not retrieved in sorted order (unless you `poll()` them one by one).
*   **Time Complexity**:
    *   **`add()` / `offer()` (enqueue)**: **O(log n)** because inserting a new element requires maintaining the heap property.
    *   **`remove()` / `poll()` (dequeue)**: **O(log n)** because removing the root (highest priority element) requires re-balancing the heap.
    *   **`peek()` / `element()`**: **O(1)** (constant time) as the head is always at the root.
*   **Example**:
    ```java
    import java.util.PriorityQueue;
    Queue<Integer> pq = new PriorityQueue<>();
    pq.add(15); pq.add(10); pq.add(30); pq.add(5); //
    System.out.println(pq.peek()); // Prints 5 (smallest is highest priority)

    while (!pq.isEmpty()) {
        System.out.print(pq.poll() + " "); // Prints 5 10 15 30 (elements extracted in priority order)
    }

    // Custom Comparator (reverse order for highest value as highest priority)
    pq = new PriorityQueue<>(Comparator.reverseOrder());
    pq.add(15); pq.add(10); pq.add(30); pq.add(5);
    System.out.println("\n" + pq.peek()); // Prints 30
    ```

#### 7.3. Deque Interface (Double Ended Queue)

*   **Definition**: An interface that extends `Queue` and represents a **double-ended queue**. It allows insertions and deletions from **both ends** (front and rear).
*   **Versatility**: Can function as both a **Queue (FIFO)** and a **Stack (LIFO)**.
*   **Key Methods**:
    *   **Insertion**: `addFirst()`, `addLast()`, `offerFirst()`, `offerLast()`.
    *   **Removal**: `removeFirst()`, `removeLast()`, `pollFirst()`, `pollLast()`.
    *   **Examination**: `getFirst()`, `getLast()`, `peekFirst()`, `peekLast()`.
    *   **Stack Operations**: `push()` (equivalent to `addFirst()`), `pop()` (equivalent to `removeFirst()`).

#### 7.3.1. ArrayDeque

*   **Definition**: A resizable array implementation of the `Deque` interface. It is designed to be **faster than `Stack` (when used as a stack)** and **faster than `LinkedList` (when used as a queue)**.
*   **Internal Implementation**: Internally uses a **circular array**. This allows elements to be added or removed from both ends efficiently without the need for element shifting or pointer management overhead.
*   **Key Characteristics**:
    *   **No Nulls**: Does not allow null elements.
    *   **Efficient**: Fast iteration and element access due to contiguous memory allocation (array-backed).
    *   **Low Memory Overhead**: No node objects (like in `LinkedList`), just an array.
    *   **Dynamic Sizing**: The internal array doubles in size when full.
*   **Use Case**: **Recommended general-purpose `Deque` implementation**. Use `LinkedList` only if you need frequent insertions/deletions in the middle.
    ```java
    import java.util.ArrayDeque;
    import java.util.Deque;

    Deque<Integer> arrayDeque = new ArrayDeque<>(); //
    arrayDeque.addFirst(10); // Adds at front
    arrayDeque.addLast(20);  // Adds at end
    arrayDeque.offerFirst(5); // Adds at front, returns boolean
    arrayDeque.offerLast(25); // Adds at end, returns boolean
    System.out.println(arrayDeque); // Prints
    System.out.println(arrayDeque.getFirst()); // Prints 5
    System.out.println(arrayDeque.pop()); // Removes and returns 5 (stack pop)
    System.out.println(arrayDeque.pollLast()); // Removes and returns 25 (deque poll from last)
    System.out.println(arrayDeque); // Prints
    ```

#### 7.3.2. LinkedList (as Deque)

*   `LinkedList` also implements the `Deque` interface. While it offers O(1) additions/removals at both ends, its performance for iteration and general use as a deque is generally **slower than `ArrayDeque`** due to higher memory overhead and non-contiguous memory.
*   It's preferred only when **frequent insertions or deletions in the middle** of the deque are required.

#### 7.4. BlockingQueue Interface

*   **Definition**: An interface that extends `Queue` and represents a **thread-safe queue that supports blocking operations**.
*   **Purpose**: Essential for **producer-consumer problems** and other concurrent programming patterns. It simplifies communication between threads by providing automatic waiting mechanisms.
*   **Blocking Behavior**:
    *   **When Queue is Full**: `put()` method **blocks** the producing thread until space becomes available in the queue.
    *   **When Queue is Empty**: `take()` method **blocks** the consuming thread until an element becomes available in the queue.
*   **Non-Blocking Alternatives (for `add`/`remove`/`element`/`peek`)**:
    *   `offer()`: Inserts an element, returning `false` if the queue is full (doesn't block). Can also take a timeout.
    *   `poll()`: Retrieves and removes an element, returning `null` if the queue is empty (doesn't block). Can also take a timeout.
*   **Standard Queue vs. BlockingQueue**: Standard queues (like `LinkedList` as queue) do not block; operations like `add()` on a full queue or `remove()` on an empty queue will immediately throw an exception. `BlockingQueue` waits.

#### 7.4.1. ArrayBlockingQueue

*   **Definition**: A **bounded** blocking queue backed by a circular array. The capacity is fixed at creation.
*   **Single Lock**: Uses a **single lock** for both enqueue (`add`/`put`/`offer`) and dequeue (`remove`/`poll`/`take`) operations. This means only **one producer or one consumer** can operate on the queue at a time.
*   **Throughput**: Can become a **bottleneck with many threads** due to contention over the single lock.
*   **Use Case**: Suitable for scenarios with **fewer threads** where the blocking behavior is desired.

#### 7.4.2. LinkedBlockingQueue

*   **Definition**: An **optionally bounded** blocking queue backed by a linked list. If no capacity is specified, it defaults to `Integer.MAX_VALUE` (unbounded).
*   **Two Separate Locks**: Uses **two separate locks** (one for enqueue operations and one for dequeue operations).
*   **Throughput**: This allows for **higher throughput** as one producer and one consumer can operate concurrently without blocking each other, even with many threads.
*   **Use Case**: Preferred over `ArrayBlockingQueue` when **more threads** are involved, or when flexibility in capacity is needed.

#### 7.4.3. PriorityBlockingQueue

*   **Definition**: An **unbounded** blocking queue that orders its elements according to their natural order or a `Comparator`. It is the **thread-safe version of `PriorityQueue`**.
*   **Key Characteristics**:
    *   **Unbounded (by default)**: `put()` method will **never block** as there is always space available (unless memory runs out).
    *   **Priority-based Ordering**: The head element is always the highest priority (like `PriorityQueue`).
    *   **Not Internally Sorted**: Like `PriorityQueue`, the elements within `PriorityBlockingQueue` are not kept in sorted order; only the head is guaranteed to be the element with highest priority.
*   **Internal Implementation**: Uses a **binary heap** (represented as an array).
*   **Use Case**: For concurrent scenarios where **elements need to be processed based on priority**.

#### 7.4.4. SynchronousQueue

*   **Definition**: A **specialized blocking queue** with a capacity of **at most one element**. It acts as a **hand-off point** between producer and consumer threads.
*   **Key Characteristics**:
    *   **Zero Capacity**: It doesn't actually store elements.
    *   **Rendezvous**: Each `insert` operation (`put()`) must wait for a corresponding `remove` operation (`take()`), and vice versa. It facilitates a "direct handoff".
*   **Use Case**: Ideal for scenarios where producers and consumers need to meet to exchange a single item, ensuring synchronous data transfer without buffering.

#### 7.4.5. DelayQueue

*   **Definition**: An **unbounded `BlockingQueue`** that stores elements that implement the `Delayed` interface.
*   **Time-Based Retrieval**: Elements can **only be taken from the queue when their delay has expired**.
*   **Internal Implementation**: Internally uses a **`PriorityQueue`** to manage elements based on their remaining delay.
*   **Key Characteristics**:
    *   **Thread-Safe**: Designed for concurrent use.
    *   **Unbounded**: `put()` method never blocks.
    *   **`Delayed` Interface**: Elements must implement `Delayed` (which provides `getDelay()` and `compareTo()` methods for ordering by delay).
*   **Use Case**: Primarily used for **task scheduling** or implementing caches with expiry times.
    ```java
    import java.util.concurrent.BlockingQueue;
    import java.util.concurrent.DelayQueue;
    import java.util.concurrent.Delayed;
    import java.util.concurrent.TimeUnit;

    class DelayedTask implements Delayed {
        private String name;
        private long startTime; // When the task is ready to be processed

        public DelayedTask(String name, long delayMillis) {
            this.name = name;
            this.startTime = System.currentTimeMillis() + delayMillis; //
        }

        @Override
        public long getDelay(TimeUnit unit) {
            // Returns the remaining delay (negative if expired)
            long diff = startTime - System.currentTimeMillis();
            return unit.convert(diff, TimeUnit.MILLISECONDS);
        }

        @Override
        public int compareTo(Delayed other) {
            // Compares based on remaining delay
            return Long.compare(this.getDelay(TimeUnit.MILLISECONDS),
                                 other.getDelay(TimeUnit.MILLISECONDS));
        }

        @Override
        public String toString() {
            return name;
        }
    }

    // Main method to demonstrate
    BlockingQueue<DelayedTask> delayQueue = new DelayQueue<>();
    delayQueue.put(new DelayedTask("Task 1", 5000)); // 5-second delay
    delayQueue.put(new DelayedTask("Task 2", 3000)); // 3-second delay
    delayQueue.put(new DelayedTask("Task 3", 10000)); // 10-second delay

    while (!delayQueue.isEmpty()) {
        DelayedTask task = delayQueue.take(); // Blocks until a task's delay expires
        System.out.println("Executed: " + task);
    }
    // Output will be: Task 2, Task 1, Task 3 (in order of delay expiration)
    ```

#### 7.5. Non-Blocking Thread-Safe Queues

Sometimes, blocking threads is not desired, but thread-safety is still required.
*   **`ConcurrentLinkedQueue`**:
    *   **Definition**: An **unbounded, thread-safe, non-blocking** implementation of the `Queue` interface.
    *   **Key Characteristics**:
        *   **Lock-Free**: Uses **Compare-And-Swap (CAS) operations** internally instead of explicit locks for most operations. This allows multiple threads to add and remove elements concurrently without blocking each other.
        *   **High Throughput**: Designed for high-concurrency scenarios.
        *   **Unbounded**: Capacity grows dynamically.
    *   **Use Case**: For producer-consumer scenarios where **high performance and non-blocking behavior** are critical, and buffering is acceptable.
    ```java
    import java.util.concurrent.ConcurrentLinkedQueue;
    import java.util.Queue;

    Queue<String> taskQueue = new ConcurrentLinkedQueue<>(); //
    // Multiple producers can safely add tasks, multiple consumers can safely take tasks without blocking each other.
    ```
*   **`ConcurrentLinkedDeque`**:
    *   **Definition**: An **unbounded, thread-safe, non-blocking** implementation of the `Deque` interface.
    *   **Key Characteristics**: Similar to `ConcurrentLinkedQueue` but supports operations from both ends. Uses **CAS operations** for thread-safety.
    *   **Use Case**: When a **double-ended queue is needed in a highly concurrent, non-blocking environment**.
    ```java
    import java.util.concurrent.ConcurrentLinkedDeque;
    import java.util.Deque;

    Deque<String> concurrentDeque = new ConcurrentLinkedDeque<>(); //
    concurrentDeque.addFirst("Element0");
    concurrentDeque.addLast("Element1");
    // Safe for concurrent access.
    ```

### 8. Iterator

The `Iterator` interface (`java.util.Iterator`) is fundamental for traversing collections.
*   **`Iterable` Interface**: The `Collection` interface extends `Iterable`. Any class that implements `Iterable` (like `ArrayList`, `LinkedList`, `HashSet`, etc.) provides an `iterator()` method that returns an `Iterator` object.
*   **`for-each` Loop (Syntactic Sugar)**: The enhanced `for` loop (or `for-each` loop) in Java is internally translated by the compiler to use an `Iterator`.
*   **`Iterator` Methods**:
    *   **`hasNext()`**: Returns `true` if the iteration has more elements.
    *   **`next()`**: Returns the next element in the iteration and advances the iterator.
    *   **`remove()`**: **Removes the last element returned by `next()` from the underlying collection**. This is the **only safe way to modify a collection during iteration** without throwing a `ConcurrentModificationException`.
        ```java
        import java.util.ArrayList;
        import java.util.Iterator;
        import java.util.List;

        List<Integer> numbers = new ArrayList<>(List.of(1, 2, 3, 4, 5));
        // Using for-each with direct remove will throw ConcurrentModificationException:
        // for (Integer num : numbers) {
        //     if (num % 2 == 0) {
        //         numbers.remove(num);
        //     }
        // }

        // Using Iterator.remove() is safe during iteration
        Iterator<Integer> iterator = numbers.iterator();
        while (iterator.hasNext()) {
            Integer num = iterator.next();
            if (num % 2 == 0) {
                iterator.remove(); // Safely removes the element
            }
        }
        System.out.println(numbers); // Prints
        ```
*   **`ListIterator`**: A specialized `Iterator` for `List` implementations (`ArrayList`, `LinkedList`). It provides additional features:
    *   **Bi-directional traversal**: `hasPrevious()`, `previous()`.
    *   **Element modification**: `set(E e)` (replaces the last element returned by `next()` or `previous`).
    *   **Element insertion**: `add(E e)` (inserts at the current position).
    *   `nextIndex()`, `previousIndex()`.

### 9. Streams (Java 8+)

**Streams** are a powerful feature introduced in **Java 8** to process collections in a **functional and declarative manner**.
*   **Motivation (Why Streams?)**:
    *   **Minimal and Concise Code**: Reduces boilerplate code (loops, if/else) often required for data processing.
    *   **Functional Programming Support**: Introduces functional programming constructs (like Lambdas, Method References) to Java.
    *   **Improved Readability and Maintainability**: Makes code easier to read and understand.
    *   **Parallelism**: Simplifies achieving parallelism for large datasets without explicit multi-threading complexity.
*   **What is a Stream?**: A **sequence of elements** that supports various operations to perform computations. It's not a data structure itself; it doesn't store data. Think of it as a **pipeline for data processing**.
*   **Stream Pipeline**: Stream operations are typically chained together to form a pipeline:
    1.  **Source**: The collection or data from which the stream is created (e.g., List, Array).
    2.  **Intermediate Operations**: Transform one stream into another stream (e.g., `filter`, `map`, `sorted`). These are **lazy** and don't execute until a terminal operation is called.
    3.  **Terminal Operation**: Produces a result or a side effect (e.g., `collect`, `count`, `forEach`). This operation **triggers the execution** of all preceding intermediate operations.

#### 9.1. Creating Streams

*   **From Collections**: The most common way, by calling `stream()` on any `Collection`.
    ```java
    List<Integer> numbers = List.of(1, 2, 3, 4, 5);
    java.util.stream.Stream<Integer> streamFromList = numbers.stream(); //
    ```
*   **From Arrays**: Use `Arrays.stream()`.
    ```java
    String[] namesArray = {"Akshit", "Ram"};
    java.util.stream.Stream<String> streamFromArray = java.util.Arrays.stream(namesArray); //
    ```
*   **From Values**: Use `Stream.of()`.
    ```java
    java.util.stream.Stream<String> streamOfValues = java.util.stream.Stream.of("A", "B", "C"); //
    ```
*   **Infinite Streams**:
    *   **`Stream.generate(Supplier<T> s)`**: Creates an infinite sequential unordered stream where each element is generated by the provided `Supplier`.
        ```java
        java.util.stream.Stream<Integer> infiniteOnes = java.util.stream.Stream.generate(() -> 1); //
        infiniteOnes.limit(10).forEach(System.out::print); // Prints 1111111111
        ```
    *   **`Stream.iterate(T seed, UnaryOperator<T> f)`**: Creates an infinite sequential ordered stream where `seed` is the first element, and subsequent elements are produced by applying the `UnaryOperator` to the previous element.
        ```java
        // Generates an infinite stream of 1, 2, 3, ...
        java.util.stream.Stream<Integer> naturalNumbers = java.util.stream.Stream.iterate(1, n -> n + 1);
        naturalNumbers.limit(5).forEach(System.out::print); // Prints 12345
        ```

#### 9.2. Functional Interfaces (Pre-requisites for Streams)

Streams heavily rely on functional interfaces, which are interfaces with a **single abstract method**. They can be implemented concisely using **Lambda Expressions**.

*   **Lambda Expressions**: An **anonymous function** (no name, no return type, no access modifier).
    *   **Syntax**: `(parameters) -> { body }`.
    *   Can omit parentheses for single parameter, curly braces for single expression (return implied).
    ```java
    // Traditional
    Runnable r = new Runnable() { public void run() { System.out.println("Hello"); } };
    // Lambda Expression
    Runnable r2 = () -> System.out.println("Hello");
    ```

*   **Predicate (`java.util.function.Predicate<T>`)**:
    *   **Purpose**: Represents a **boolean-valued function** of one argument. Used for **conditions or filtering**.
    *   **Abstract Method**: `boolean test(T t)`.
    *   **Default Methods**: `and()`, `or()`, `negate()` for combining predicates.
    ```java
    Predicate<Integer> isEven = num -> num % 2 == 0; //
    System.out.println(isEven.test(4)); // Prints true

    Predicate<String> startsWithA = s -> s.startsWith("A"); //
    Predicate<String> endsWithT = s -> s.endsWith("t");
    Predicate<String> combined = startsWithA.and(endsWithT); //
    System.out.println(combined.test("Akshit")); // Prints true
    ```

*   **Function (`java.util.function.Function<T, R>`)**:
    *   **Purpose**: Represents a function that **accepts one argument and produces a result**. Used for **transformations or mapping**.
    *   **Abstract Method**: `R apply(T t)`.
    *   **Default Methods**: `andThen()` (applies first function then second), `compose()` (applies second function then first). `identity()` (static, returns a function that returns its input).
    ```java
    Function<Integer, Integer> doubleIt = num -> num * 2; //
    System.out.println(doubleIt.apply(10)); // Prints 20

    Function<Integer, Integer> tripleIt = num -> num * 3;
    // (20 * 2) * 3 = 120
    Function<Integer, Integer> doubleThenTriple = doubleIt.andThen(tripleIt); //
    System.out.println(doubleThenTriple.apply(20)); // Prints 120
    // (20 * 3) * 2 = 120
    Function<Integer, Integer> tripleThenDouble = doubleIt.compose(tripleIt); //
    System.out.println(tripleThenDouble.apply(20)); // Prints 120
    ```

*   **Consumer (`java.util.function.Consumer<T>`)**:
    *   **Purpose**: Represents an operation that **accepts a single input argument and returns no result** (performs an action).
    *   **Abstract Method**: `void accept(T t)`.
    *   **Default Method**: `andThen()` (applies first consumer then second).
    ```java
    Consumer<Integer> printNum = num -> System.out.println("Consumed: " + num); //
    printNum.accept(50); // Prints "Consumed: 50"
    ```

*   **Supplier (`java.util.function.Supplier<T>`)**:
    *   **Purpose**: Represents an operation that **supplies a result** without accepting any input arguments.
    *   **Abstract Method**: `T get()`.
    ```java
    Supplier<String> helloSupplier = () -> "Hello World"; //
    System.out.println(helloSupplier.get()); // Prints "Hello World"
    ```

*   **Bi-Variants**: Functional interfaces for operations taking two arguments.
    *   **`BiPredicate<T, U>`**: `boolean test(T t, U u)` [14>`)**:
    *   Specialized `BiFunction` where **all three types (two inputs, one output) are the same**. `T apply(T t1, T t2)`.

#### 9.3. Method Reference (`::`)

*   **Purpose**: A **shorthand syntax for lambda expressions**. It allows you to **refer to a method without executing it**, treating it as a function itself.
*   **Types**:
    *   **Static Method Reference**: `ClassName::staticMethodName`
        ```java
        // Lambda: list.forEach(num -> System.out.println(num));
        list.forEach(System.out::println); //
        ```
    *   **Instance Method Reference (on a particular object)**: `objectName::instanceMethodName`
    *   **Instance Method Reference (on an arbitrary object of a particular type)**: `ClassName::instanceMethodName`
        ```java
        // Lambda: names.stream().map(s -> s.toUpperCase());
        names.stream().map(String::toUpperCase); //
        ```
    *   **Constructor Reference**: `ClassName::new`. Used to create new objects.
        ```java
        // Lambda: names.stream().map(name -> new MobilePhone(name));
        names.stream().map(MobilePhone::new); //
        ```

#### 9.4. Intermediate Operations (Lazy)

Intermediate operations transform a stream into another stream. They are **lazy**, meaning they are not executed until a terminal operation is invoked on the stream.
*   **`filter(Predicate<T> predicate)`**: Returns a stream consisting of the elements that match the given predicate.
    ```java
    names.stream().filter(name -> name.startsWith("A")); //
    ```
*   **`map(Function<T, R> mapper)`**: Returns a stream consisting of the results of applying the given function to the elements of this stream.
    ```java
    names.stream().map(String::toUpperCase); //
    ```
*   **`sorted()` / `sorted(Comparator<T> comparator)`**: Returns a stream consisting of the elements of this stream, sorted according to natural order or a provided `Comparator`.
*   **`distinct()`**: Returns a stream consisting of the distinct elements of this stream (removes duplicates).
*   **`limit(long maxSize)`**: Returns a stream consisting of the elements of this stream, truncated to be no longer than `maxSize`.
*   **`skip(long n)`**: Returns a stream consisting of the remaining elements of this stream after discarding the first `n` elements.
*   **`peek(Consumer<T> action)`**: Performs an action on each element as elements are consumed from the stream. It's primarily used for **debugging** or side effects, as it doesn't change the stream's elements.
*   **`flatMap(Function<T, Stream<R>> mapper)`**: Transforms each element of a stream into another stream and then **flattens** the resulting streams into a single stream. Used when individual elements of a stream are themselves collections or can generate multiple values.
    ```java
    List<List<String>> listOfLists = List.of(
        List.of("Apple", "Banana"),
        List.of("Orange", "Grape")
    );
    // FlatMap to combine all fruits into a single stream and convert to uppercase
    listOfLists.stream()
               .flatMap(Collection::stream) // Converts each inner list to a stream, then flattens
               .map(String::toUpperCaseEager)

Terminal operations produce a result or a side effect and **cause the intermediate operations to execute**. **A stream can only have one terminal operation**, and after it's called, the stream is considered **consumed/closed and cannot be reused**.
*   **`collect(Collector<T, A, R> collector)`**: Performs a mutable reduction operation on the elements of this stream using a `Collector`.
    *   **`Collectors` Utility Class**: Provides common implementations for `Collector` (e.g., `toList`, `toSet`, `toMap`, `groupingBy`, `joining`).
    *   **`toList()` / `toSet()` (Java 16+)**: Directly converts stream elements into a `List` or `Set`.
    ```java
    List<String> upperCaseNames = names.stream()
                                     .map(String::toUpperCase)
                                     .collect(java.util.stream.Collectors.toList()); //
    // Or directly with Java 16+
    List<String> upperCaseNames2 = names.stream()
                                      .map(String::toUpperCase)
                                      .toList();
    ```
    *   **`joining()`**: Concatenates elements of a `CharSequence` stream into a single string. Can specify delimiter, prefix, and suffix.
        ```java
        String joinedNames = names.stream()
                                .map(String::toUpperCase)
                                .collect(java.util.stream.Collectors.joining(", ")); //
        ```
    *   **`counting()`**: Returns a `Collector` that counts the number of input elements.
    *   **`summarizingInt/Long/Double()`**: Returns a `Collector` that applies an `IntFunction` to each input element and returns an `IntSummaryStatistics` (or `Long/Double`) object containing count, sum, min, average, and max.
    *   **`groupingBy(Function classifier)`**: Groups elements according to a classifier `Function` and returns a `Map`. Can take an optional `downstream77]
        ```
    *   **`partitioningBy(Predicate predicate)`**: Partitions elements into two groups (`Map<Boolean, List<T>>`) based on whether they match a given `Predicate`.
    *   **`toMap(Function keyMapper, Function valueMapper)`**: Collects elements into a `Map`. Can take a `mergeFunction` for duplicate keys.
        ```java
        Map<String, Integer> fruitLengths = List.of("Apple", "Banana", "Cherry").stream()
                                              .collect(java.util.stream.Collectors.toMap(
                                                  name -> name, // Key is the fruit name
                                                  String::length // Value is its length
                                              ));
        ```
*   **`forEach(Consumer<T> action)`**: Performs an action for each element of the stream. Does not return a new stream.
    ```java
    names.stream().forEach(System.out::println); //
    ```
*   **`reduce(BinaryOperator<T> accumulator)` / `reduce(T identity, BinaryOperator<T> accumulator)`**: Performs a reduction on the elements of this stream, using an associative accumulation function, and returns an `Optional<T>`.
    ```java
    Optional<Integer> sum = List.of(1, 2, 3, 4, 5).stream().reduce(Integer::sum); //
    System.out.println(sum.get()); // Prints 15
    ```
*   **`count()`**: Returns the count of elements in this stream [15`, `findAny`)**: Both return an `Optional<T>` and are **short-circuiting**.
    *   `findFirst()`: Returns an `Optional` containing the first element of the stream (useful for ordered streams).
    *   `findAny()`: Returns an `Optional` containing any element from the stream (useful for parallel streams where order doesn't matter).
*   **`toArray()`**: Returns an array containing the elements of this stream.
*   **`min(Comparator<T> comparator)` / `max(Comparator<T> comparator)`**: Returns an `Optional<T>` describing the minimum/maximum element of this stream according to the provided `Comparator`.

#### 9.6. Parallel Streams

*   **Definition**: A type of stream that enables **parallel processing**, allowing **multiple threads to work on different parts of the stream concurrently**.
*   **Creation**: Obtained by calling `parallelStream()` on a `Collection` or `parallel()` on an existing stream.
    ```java
    List<Integer> largeList = new ArrayList<>(); // fill with 20000 numbers
    // Sequential Stream
    long startTime = System.currentTimeMillis();
    largeList.stream().map(num -> calculateFactorial(num)).toList();
    long sequentialTime = System.currentTimeMillis() - startTime;
    System.out.println("Sequential time: " + sequentialTime + " ms"); // e.g., 150 ms

    // Parallel Stream
    startTime = System.currentTimeMillis();
    largeList.parallelStream().map(num ->'s processing shouldn't depend on another's order).
*   **Pitfalls**:
    *   For **small datasets** or **I/O-intensive tasks**, parallel streams might be slower due to the overhead of managing threads.
    *   Can lead to **incorrect results** if tasks are **dependent on order or shared mutable state**. (e.g., cumulative sum example will give wrong results in parallel stream).
*   **`sequential()` Method**: Converts a parallel stream back to a sequential stream.
*   **`forEachOrdered(Consumer<T> action)`**: When using `forEach` on a parallel stream, the order of processing is not guaranteed. `forEachOrdered` ensures that the action is performed in the **encounter order** of the stream, even if the stream is parallel.

#### 9.7. Primitive Streams (`IntStream`, `LongStream`, `DoubleStream`)

*   **Purpose**: Specialized streams for **primitive integer, long, and double types**. They help.
    ```java
    import java.util.stream.IntStream;
    // Range (exclusive end)
    IntStream.range(1, 5).forEach(System.out::print); // Prints 1234
    // Range (inclusive end)
    IntStream.rangeClosed(1, 5).forEach(System.out::print); // Prints 12345
    ```
    *   From `Random` class: `new Random().ints(count)`.
*   **Common Methods**: Primitive streams have methods for common reductions like `sum()`, `average()`, `min()`, `max()`, and `summaryStatistics()`.
*   **Conversion**:
    *   **`boxed()`**: Converts a primitive stream (e.g., `IntStream`) to a `Stream` of its corresponding wrapper type (e.g., `Stream<Integer>`). This is needed to use collectors like `toList()` which expect `Stream<T>`.
    ```java
    List-on practice.

**Analogy**: Think of the **Java Collections Framework** as a diverse set of specialized containers in a highly organized kitchen. Each container (like an `ArrayList`, `LinkedList`, `HashMap`, or `TreeMap`) is designed for a specific purpose – some are good for ordered items, some for unique items, some for quick lookups, and some even come with built-in safeguards for multiple chefs working simultaneously. The **Streams API** is like a fancy, automated food preparation line you can attach to any of these containers. Instead of manually moving ingredients from one bowl to another, chopping, dicing, and mixing (traditional loops and if/else), you just declare *what* you want to happen (e.g., "filter out the rotten fruit, then dice the rest, then collect them in a serving bowl"), and the preparation line efficiently handles all the steps, even parallelizing them for large batches without you needing to manage individual kitchen hands.
