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


