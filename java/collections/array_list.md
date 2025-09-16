Got it 👍
Here’s your notes properly formatted into clean Markdown (fixed indentation, removed stray `<br>`, corrected broken import, and unified sectioning):

---

# List Interface and ArrayList in Java

## 1. The `List` Interface

The `List` interface is part of the Java Collections Framework and **extends the `Collection` interface**.
It provides a blueprint for data structures that maintain an **ordered sequence of elements** and allow **duplicate elements**.

### Key Features

* **Order Preservation:** Elements are stored and accessed in the order they were added.
* **Index-Based Access:** Elements can be accessed using their index (like arrays).
* **Allows Duplicates:** Multiple identical elements can be stored.

### Common Methods

Inherited from `Collection`:

* `size()`, `isEmpty()`, `contains(element)`, `add(element)`, `remove(element)`

### When to Use

Use `List` when you need **insertion order** and **duplicates**.

---

## 2. `ArrayList` – A Dynamic Array Implementation

`ArrayList` is a **class that implements the `List` interface**. Unlike traditional arrays (fixed size), `ArrayList` **resizes dynamically**.

### Internal Working

* Stores elements in an internal **Object\[] array**.
* When full, creates a new array (**1.5× capacity**) and copies elements (**O(n)**).
* Removing shifts elements (**O(n)** if at start).

### Capacity vs Size

* **Capacity:** Size of the backing array.
* **Size:** Actual number of elements stored.
* Default capacity: **10** (can specify at creation).

### Example: Creating an `ArrayList`

```java
import java.util.ArrayList;
import java.util.List;

public class ArrayListExample {
    public static void main(String[] args) {
        ArrayList<Integer> myArrayList = new ArrayList<>(); 
        List<String> fruits = new ArrayList<>();

        System.out.println("Initial size: " + myArrayList.size()); // 0

        List<String> largeList = new ArrayList<>(1000);
        System.out.println("Initial size of largeList: " + largeList.size()); // 0
    }
}
```

---

## 3. Basic Operations with `ArrayList`

### 3.1 Adding Elements

* `add(e)` → adds to end
* `add(index, e)` → inserts at index

```java
fruits.add("Apple");
fruits.add(1, "Grape");
fruits.addAll(List.of("Mango", "Orange"));
```

---

### 3.2 Accessing Elements

* `get(index)` → returns element
* `size()` → returns list size

```java
System.out.println(numbers.get(0));
System.out.println(numbers.size());
```

---

### 3.3 Iterating

```java
for (int i = 0; i < numbers.size(); i++) {
    System.out.println(numbers.get(i));
}

for (Integer num : numbers) {
    System.out.println(num);
}
```

---

### 3.4 Checking Existence

```java
numbers.contains(5);  // true
```

---

### 3.5 Modifying Elements

```java
numbers.set(2, 50);
```

---

### 3.6 Removing Elements

* `remove(index)` → removes element at index
* `remove(Object o)` → removes first occurrence

⚠️ With `Integer`, use `remove(Integer.valueOf(x))` to avoid confusion with index.

---

## 4. Capacity Management

* **Set initial capacity**: `new ArrayList<>(1000)`
* **Trim unused space**: `trimToSize()`

---

## 5. Common `ArrayList` Methods

| Method           | Syntax                   | Description                    | Example                      |
| ---------------- | ------------------------ | ------------------------------ | ---------------------------- |
| **`add()`**      | `add(e)`, `add(i, e)`    | Adds element to end / at index | `fruits.add("Apple");`       |
| **`get()`**      | `get(i)`                 | Returns element at index       | `fruits.get(1);`             |
| **`set()`**      | `set(i, e)`              | Replaces element at index      | `fruits.set(1, "Cherry");`   |
| **`remove()`**   | `remove(i)`, `remove(o)` | Removes by index or object     | `fruits.remove("Apple");`    |
| **`size()`**     | `size()`                 | Returns count                  | `fruits.size();`             |
| **`clear()`**    | `clear()`                | Removes all                    | `fruits.clear();`            |
| **`contains()`** | `contains(o)`            | Checks existence               | `fruits.contains("Banana");` |
| **`indexOf()`**  | `indexOf(o)`             | Returns first index / -1       | `fruits.indexOf("Cherry");`  |
| **`isEmpty()`**  | `isEmpty()`              | Returns `true` if empty        | `fruits.isEmpty();`          |

---

## 6. Other Useful Methods

| Method            | Syntax                        | Description                       |
| ----------------- | ----------------------------- | --------------------------------- |
| **`addAll()`**    | `addAll(c)`                   | Adds all elements from collection |
| **`removeAll()`** | `removeAll(c)`                | Removes all matching elements     |
| **`iterator()`**  | `iterator()`                  | Iterates over list                |
| **`toArray()`**   | `toArray()`, `toArray(T[] a)` | Converts list to array            |

---

## 7. Complete Example

```java
import java.util.ArrayList;

public class ArrayListDemo {
    public static void main(String[] args) {
        ArrayList<String> animals = new ArrayList<>();

        animals.add("Dog");
        animals.add("Cat");
        animals.add("Mouse");
        animals.add(1, "Tiger");

        System.out.println("Initial: " + animals);
        System.out.println("Size: " + animals.size());
        System.out.println("Element at index 2: " + animals.get(2));

        System.out.println("Contains 'Cat'? " + animals.contains("Cat"));
        System.out.println("Index of 'Dog': " + animals.indexOf("Dog"));

        animals.set(2, "Lion");
        System.out.println("After set: " + animals);

        animals.remove("Dog");
        animals.remove(0);
        System.out.println("After remove: " + animals);

        animals.clear();
        System.out.println("After clear: " + animals);
        System.out.println("Is empty? " + animals.isEmpty());
    }
}
```

**Output:**

```
Initial: [Dog, Tiger, Cat, Mouse]
Size: 4
Element at index 2: Cat
Contains 'Cat'? true
Index of 'Dog': 0
After set: [Dog, Tiger, Lion, Mouse]
After remove: [Lion, Mouse]
After clear: []
Is empty? true
```

---
Of course. Based on the provided sources, here are comprehensive notes and a coding example for `ArrayList` in Java.

### Notes on Java `ArrayList`

#### **1. Core Concepts and Features**

*   **Hierarchy**: `ArrayList` is a class that implements the `List` interface, which in turn extends the `Collection` interface.
*   **Dynamic Size**: Unlike regular arrays which have a fixed size defined at creation, an `ArrayList` can **dynamically grow and shrink** to accommodate the number of elements it holds.
*   **Ordered Collection**: An `ArrayList` **preserves the insertion order** of elements. The order in which you add elements is the order in which they are stored and retrieved.
*   **Allows Duplicates**: You can store duplicate elements in an `ArrayList`.
*   **Index-Based Access**: Elements can be accessed directly using their zero-based index, similar to a standard array.
*   **Generics**: `ArrayList` is a generic class, meaning you should specify the type of objects it will store (e.g., `ArrayList<Integer>`). This ensures type safety.

#### **2. Internal Mechanics: Capacity vs. Size**

*   **Underlying Structure**: Internally, `ArrayList` uses a regular array to store its elements.
*   **Capacity**: This refers to the **length of the internal array**, indicating how many elements the list can hold *before* it needs to resize.
    *   The **default initial capacity** of a new `ArrayList` is **10**.
    *   You can specify a custom initial capacity (e.g., `new ArrayList<>(1000)`) to avoid the overhead of frequent resizing if you have an estimate of the number of elements.
*   **Size**: This is the **actual number of elements** currently stored in the `ArrayList`.
*   **Growth Mechanism**:
    1.  When you add an element, `ArrayList` checks if the internal array is full.
    2.  If it is full, a **new, larger array** is created. The new capacity is typically **1.5 times the old capacity**.
    3.  All elements from the old array are copied to the new one.
    4.  Finally, the new element is added.
    This resizing process has a time complexity of O(n) because of the copy operation.
*   **Shrinking**: `ArrayList` **does not automatically shrink** its capacity when elements are removed. To save memory, you can manually call the **`trimToSize()`** method, which resizes the internal array to match the current element count.

#### **3. Creating an `ArrayList`**

There are several ways to create a list, each with different characteristics:

*   **Standard Creation**: This creates a fully modifiable `ArrayList`.
    `List<String> list = new ArrayList<>();`
*   **`Arrays.asList()`**: Creates a **fixed-size list**. You can modify existing elements with `set()`, but you **cannot add or remove** elements.
    `List<String> fixedList = Arrays.asList("Apple", "Banana");`
*   **`List.of()` (Java 9+)**: Creates an **unmodifiable (immutable) list**. You **cannot add, remove, or modify** elements. Any attempt to change it will result in an `UnsupportedOperationException`.
    `List<Integer> immutableList = List.of(1, 2, 3);`
*   **From Another Collection**: You can create a modifiable `ArrayList` from any existing collection, which is useful for converting a fixed-size or unmodifiable list into a dynamic one.
    `List<String> modifiableList = new ArrayList<>(fixedList);`

#### **4. Common Operations and Methods**

*   **Adding Elements**:
    *   `add(element)`: Appends an element to the end of the list.
    *   `add(index, element)`: Inserts an element at a specific index, shifting subsequent elements to the right.
    *   `addAll(collection)`: Appends all elements from another collection to the list.
*   **Accessing Elements**:
    *   `get(index)`: Retrieves the element at a specified index.
*   **Updating Elements**:
    *   `set(index, element)`: **Replaces** the element at a specified index with a new one.
*   **Removing Elements**:
    *   `remove(index)`: Removes the element at the specified index. Subsequent elements are shifted to the left.
    *   `remove(Object)`: Removes the first occurrence of the specified element.
    *   **Important Note for Integers**: When working with a list of integers, `list.remove(1)` will be interpreted as removing the element at **index 1**. To remove the **object `1`**, you must wrap it: `list.remove(Integer.valueOf(1))`.
*   **Utility Methods**:
    *   `size()`: Returns the number of elements in the list.
    *   `contains(Object)`: Returns `true` if the list contains the specified element.
    *   `toArray()`: Converts the list into an array.
    *   `Collections.sort(list)` or `list.sort(null)`: Sorts the list in place.

#### **5. Time Complexity**

*   **`get(index)`**: **O(1)** - Constant time, as access is direct.
*   **`add(element)`** (to the end): Amortized **O(1)**, but **O(n)** in the worst case when the internal array needs to be resized.
*   **`add(index, element)`**: **O(n)** - Linear time, because elements may need to be shifted.
*   **`remove(index)`**: **O(n)** - Linear time, as elements to the right of the removed element must be shifted left.

---

### Coding Example

Here is a coding example that demonstrates the creation and manipulation of an `ArrayList`, incorporating many of the concepts from the notes above.

```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.Collections;
import java.util.List;

public class ArrayListExample {
    public static void main(String[] args) {
        // 1. Creating a modifiable ArrayList
        // Using the List interface as the reference type is good practice.
        List<String> fruits = new ArrayList<>();

        // 2. Adding elements
        fruits.add("Apple");
        fruits.add("Banana");
        fruits.add("Cherry");
        System.out.println("Initial list: " + fruits); // Prints the list using its toString() method

        // 3. Adding an element at a specific index
        fruits.add(1, "Orange"); // Inserts "Orange" at index 1
        System.out.println("After adding at index 1: " + fruits);

        // 4. Accessing an element
        String firstFruit = fruits.get(0);
        System.out.println("First fruit: " + firstFruit);

        // 5. Updating an element
        fruits.set(2, "Mango"); // Replaces "Banana" with "Mango"
        System.out.println("After setting index 2: " + fruits);

        // 6. Checking size and existence
        System.out.println("Current size: " + fruits.size());
        boolean hasApple = fruits.contains("Apple");
        System.out.println("Contains 'Apple'? " + hasApple);

        // 7. Removing elements
        // Remove by index
        fruits.remove(3); // Removes "Cherry" at index 3
        System.out.println("After removing element at index 3: " + fruits);

        // Remove by object
        fruits.remove("Apple"); // Removes the first occurrence of "Apple"
        System.out.println("After removing 'Apple' object: " + fruits);
        
        // 8. Iterating through the list
        System.out.println("Iterating with for-each loop:");
        for (String fruit : fruits) {
            System.out.println("- " + fruit);
        }

        // 9. Sorting the list
        Collections.sort(fruits);
        System.out.println("Sorted list: " + fruits);
        
        // 10. Converting List to Array
        // The new String argument tells the method the desired array type.
        String[] fruitArray = fruits.toArray(new String);
        System.out.println("Converted to Array: " + Arrays.toString(fruitArray));
    }
}
```

**Output of the Example:**

```
Initial list: [Apple, Banana, Cherry]
After adding at index 1: [Apple, Orange, Banana, Cherry]
First fruit: Apple
After setting index 2: [Apple, Orange, Mango, Cherry]
Current size: 4
Contains 'Apple'? true
After removing element at index 3: [Apple, Orange, Mango]
After removing 'Apple' object: [Orange, Mango]
Iterating with for-each loop:
- Orange
- Mango
Sorted list: [Mango, Orange]
Converted to Array: [Mango, Orange]
```

