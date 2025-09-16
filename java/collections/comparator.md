Got it 👍 Let’s go through **Java Comparator** in detail with clear notes and coding examples.

---

# 📘 Java Comparator

## 1. What is Comparator?

* **Comparator** is an interface in `java.util` package.
* It is used to define **custom ordering** of objects.
* Unlike `Comparable`, where the class itself defines the natural ordering, `Comparator` allows us to **separate sorting logic** from the class.

---

## 2. Comparator Interface

```java
@FunctionalInterface
public interface Comparator<T> {
    int compare(T o1, T o2);
}
```

### Method:

* `int compare(T o1, T o2)`

  * Returns:

    * negative integer → `o1 < o2`
    * zero → `o1 == o2`
    * positive integer → `o1 > o2`

---

## 3. Example: Sorting with Comparator

```java
import java.util.*;

class Student {
    int id;
    String name;

    Student(int id, String name) {
        this.id = id;
        this.name = name;
    }

    public String toString() {
        return id + " - " + name;
    }
}

class NameComparator implements Comparator<Student> {
    public int compare(Student s1, Student s2) {
        return s1.name.compareTo(s2.name); // alphabetical order
    }
}

class IdComparator implements Comparator<Student> {
    public int compare(Student s1, Student s2) {
        return Integer.compare(s1.id, s2.id); // numerical order
    }
}

public class Main {
    public static void main(String[] args) {
        List<Student> list = new ArrayList<>();
        list.add(new Student(3, "Ravi"));
        list.add(new Student(1, "Amit"));
        list.add(new Student(2, "Karan"));

        Collections.sort(list, new NameComparator());
        System.out.println("Sorted by Name: " + list);

        Collections.sort(list, new IdComparator());
        System.out.println("Sorted by Id: " + list);
    }
}
```

---

## 4. Anonymous Class / Lambda with Comparator

Instead of creating separate comparator classes, we can use **lambda expressions**:

```java
Collections.sort(list, (s1, s2) -> s1.name.compareTo(s2.name));

Collections.sort(list, (s1, s2) -> Integer.compare(s1.id, s2.id));
```

---

## 5. Comparator Utility Methods (Java 8+)

Java 8 introduced **default and static methods** in Comparator.

### Common Methods:

1. **`comparing()`**
   Creates a comparator based on a function.

   ```java
   Collections.sort(list, Comparator.comparing(s -> s.name));
   ```

2. **`thenComparing()`**
   Used for multiple-level sorting (tie-breakers).

   ```java
   Collections.sort(list,
       Comparator.comparing((Student s) -> s.name)
                 .thenComparing(s -> s.id));
   ```

3. **`reversed()`**
   Reverses the comparator order.

   ```java
   Collections.sort(list, Comparator.comparing(s -> s.id).reversed());
   ```

4. **`naturalOrder()` & `reverseOrder()`**
   Works for objects implementing Comparable.

   ```java
   List<String> names = Arrays.asList("Ravi", "Amit", "Karan");
   names.sort(Comparator.naturalOrder());  // Ascending
   names.sort(Comparator.reverseOrder());  // Descending
   ```

---

## 6. Differences: Comparable vs Comparator

| Feature        | Comparable         | Comparator               |
| -------------- | ------------------ | ------------------------ |
| Package        | `java.lang`        | `java.util`              |
| Method         | `compareTo(T o)`   | `compare(T o1, T o2)`    |
| Logic Location | Inside the class   | Outside the class        |
| Sorting Type   | Natural ordering   | Custom ordering          |
| Flexibility    | One way to compare | Multiple ways to compare |

---

✅ **Quick Recap:**

* Use **Comparable** when class has a **single natural order**.
* Use **Comparator** when you want **multiple sorting criteria** or don’t want to modify the class.
* Prefer **lambda & Comparator.comparing()** in modern Java.

---

Of course. Based on the provided video transcript, here are detailed notes and coding examples on the Java `Comparator` interface.

### Notes on Java `Comparator`

The `Comparator` is a powerful interface in Java used to define **custom sorting logic** for objects. While collections of built-in types like `String` or `Integer` have a "natural order" (alphabetical or numerical ascending), `Comparator` allows you to specify any ordering you need, such as sorting by string length or sorting custom objects by a specific attribute.

#### 1. The Core Concept: The `compare()` Method

The `Comparator` is a **functional interface** with a single abstract method: `compare(T o1, T o2)`. This method is the heart of all custom sorting. It takes two objects of the same type and returns an integer to determine their relative order.

The return value dictates the sorting outcome:
*   **Negative Integer**: `o1` should come **before** `o2` in the sorted list.
*   **Zero**: `o1` and `o2` are considered **equal** in terms of sorting order. Their relative position might be maintained.
*   **Positive Integer**: `o1` should come **after** `o2` in the sorted list (meaning `o2` comes first).

The `sort` method on a list uses this logic repeatedly on pairs of elements to arrange the entire collection correctly. You only need to define the logic for comparing two items, and the sort algorithm handles the rest.

#### 2. Three Ways to Implement a `Comparator`

The video demonstrates three primary ways to create and use a `Comparator`.

##### Method 1: Create an Implementation Class (The Traditional Way)

You can create a separate class that implements the `Comparator` interface and provides the logic for the `compare` method.

**Example: Sorting integers in descending order.**
For a descending sort, if you are comparing 5 (`o1`) and 3 (`o2`), you want 5 to come first. For `o1` to come before `o2`, the `compare` method must return a negative value. The logic `o2 - o1` (i.e., `3 - 5`) produces a negative result, achieving the desired order.

```java
import java.util.ArrayList;
import java.util.Comparator;
import java.util.List;

// 1. Define the implementation class
class MyIntegerComparator implements Comparator<Integer> {
    @Override
    public int compare(Integer o1, Integer o2) {
        // To sort in descending order, we use o2 - o1
        return o2 - o1;
    }
}

public class TraditionalExample {
    public static void main(String[] args) {
        List<Integer> numbers = new ArrayList<>(List.of(5, 1, 3, 2, 4));
        System.out.println("Original list: " + numbers);

        // 2. Pass an instance of the class to the sort method
        numbers.sort(new MyIntegerComparator());
        
        System.out.println("Sorted descending: " + numbers);
    }
}
```

##### Method 2: Use a Lambda Expression (The Modern Way)

Since `Comparator` is a functional interface, you can provide its implementation directly using a concise lambda expression. This avoids the need for a separate class.

**Example: Sorting strings by length in ascending order.**
To sort by length, we compare the lengths of the two strings. For ascending order (shortest first), if `o1`'s length is less than `o2`'s length, we need a negative result. The logic `o1.length() - o2.length()` achieves this perfectly.

```java
import java.util.ArrayList;
import java.util.List;

public class LambdaExample {
    public static void main(String[] args) {
        List<String> words = new ArrayList<>(List.of("Apple", "Date", "Banana"));
        System.out.println("Original list: " + words);

        // Use a lambda expression directly in the sort method
        // (s1, s2) are the two strings being compared
        words.sort((s1, s2) -> s1.length() - s2.length());

        System.out.println("Sorted by length (ascending): " + words); // Output: [Date, Apple, Banana]
        
        // For descending order, just flip the logic
        words.sort((s1, s2) -> s2.length() - s1.length());
        System.out.println("Sorted by length (descending): " + words); // Output: [Banana, Apple, Date]
    }
}
```

##### Method 3: Use `Comparator` Helper Methods (The Fluent Java 8+ Way)

Java 8 introduced static helper methods on the `Comparator` interface itself, allowing for a very readable, "fluent" way to build comparators, especially for complex scenarios.

*   **`Comparator.comparing(keyExtractor)`**: Creates a comparator that sorts based on a specific attribute of the object. It uses a method reference (e.g., `Student::getGpa`) to specify which attribute to use for comparison.
*   **`.reversed()`**: Reverses the natural order of the preceding comparator.
*   **`.thenComparing(keyExtractor)`**: Used for **tie-breaking**. If the primary comparison results in a zero (elements are equal), this secondary comparator is used to decide the order.

#### 3. Advanced Use Case: Sorting a List of Custom Objects

When you have a custom class like `Student`, Java doesn't know its "natural order". Trying to sort a list of students with `students.sort(null)` will throw an exception. This is where `Comparator` is essential.

**Example: Sorting `Student` objects.**
Let's sort a list of students first by GPA in descending order. If two students have the same GPA, we will sort them by name in alphabetical (ascending) order as a tie-breaker.

```java
import java.util.ArrayList;
import java.util.Comparator;
import java.util.List;

// A custom class that does not have a natural sorting order
class Student {
    private String name;
    private double gpa;

    public Student(String name, double gpa) { this.name = name; this.gpa = gpa; }
    public String getName() { return name; }
    public double getGpa() { return gpa; }
    @Override public String toString() { return name + " (" + gpa + ")"; }
}

public class CustomObjectSort {
    public static void main(String[] args) {
        List<Student> students = new ArrayList<>(List.of(
            new Student("Charlie", 3.5),
            new Student("Akshit", 3.9),
            new Student("Alice", 3.5),
            new Student("Bob", 3.7)
        ));
        
        System.out.println("Original students: " + students);
        
        // **Using Comparator Helper Methods (Recommended)**
        Comparator<Student> gpaThenNameComparator = Comparator
                .comparing(Student::getGpa) // Primary sort key: GPA (ascending by default)
                .reversed()                 // Reverse to make it descending
                .thenComparing(Student::getName); // Secondary sort key for ties: Name (ascending)

        students.sort(gpaThenNameComparator);

        System.out.println("Sorted by GPA (desc) then Name (asc): " + students);
        
        // **Implementing the same logic manually with a lambda**
        students.sort((s1, s2) -> {
            // NOTE: For doubles, direct subtraction can cause precision loss if cast to int.
            // It's safer to use Double.compare or if/else logic.
            if (s2.getGpa() > s1.getGpa()) {
                return 1; // s2 comes first
            } else if (s2.getGpa() < s1.getGpa()) {
                return -1; // s1 comes first
            } else {
                // GPAs are equal, so use the tie-breaker
                // String's compareTo method provides natural alphabetical ordering
                return s1.getName().compareTo(s2.getName());
            }
        });
        System.out.println("Sorted manually with same logic: " + students);
    }
}
```
**Output of the above code:**
```
Original students: [Charlie (3.5), Akshit (3.9), Alice (3.5), Bob (3.7)]
Sorted by GPA (desc) then Name (asc): [Akshit (3.9), Bob (3.7), Alice (3.5), Charlie (3.5)]
Sorted manually with same logic: [Akshit (3.9), Bob (3.7), Alice (3.5), Charlie (3.5)]
```
