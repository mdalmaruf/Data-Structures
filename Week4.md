# Java List: Storing Different Data Types

---

## 1. Arrays vs Lists: What's the Difference?

| Feature          | Array                             | List                                      |
| ---------------- | --------------------------------- | ----------------------------------------- |
| Size             | Fixed once created                | Dynamic (can grow/shrink)                 |
| Type Flexibility | Homogeneous (same type)           | Can be homogeneous or heterogeneous       |
| Syntax           | Simpler for primitive types       | More flexible and feature-rich            |
| Language Support | Available in both Python and Java | Native in Python, via Collections in Java |

---

## 2. Python List: Naturally Flexible

Python lists are dynamic and can hold mixed types with no additional effort.

```python
my_list = ["Alice", 25, 5.7, True, None]

for item in my_list:
    print(f"Value: {item}, Type: {type(item)}")
```

### Output:

```
Value: Alice, Type: <class 'str'>
Value: 25, Type: <class 'int'>
Value: 5.7, Type: <class 'float'>
Value: True, Type: <class 'bool'>
Value: None, Type: <class 'NoneType'>
```

---

## 3. Java Typed ArrayList vs Fixed-Size Array

### a. Fixed-Size Array

Java arrays are fixed in size and type-specific.

```java
public class FixedArrayExample {
    public static void main(String[] args) {
        String[] names = new String[2];
        names[0] = "Alice";
        names[1] = "Bob";

        for (String name : names) {
            System.out.println(name);
        }
    }
}
```

### Output:

```
Alice
Bob
```

### b. Dynamic ArrayList (Typed)

`ArrayList<String>` is a resizable array that only accepts strings.

```java
import java.util.*;

public class TypedArrayListExample {
    public static void main(String[] args) {
        ArrayList<String> names = new ArrayList<>();
        names.add("Alice");
        names.add("Bob");

        for (String name : names) {
            System.out.println(name);
        }
    }
}
```

### Output:

```
Alice
Bob
```

### Key Differences:

* **Array** has fixed size; you must declare the size at creation.
* **ArrayList** grows dynamically and provides more built-in methods.
* Both are type-specific when using generics or defining type like `String[]`.

---

In Java, `ArrayList` is used for dynamic lists, but with a specific data type (generics).

```java
import java.util.*;

public class TypedListExample {
    public static void main(String[] args) {
        List<String> names = new ArrayList<>();
        names.add("Alice");
        names.add("Bob");

        for (String name : names) {
            System.out.println(name);
        }
    }
}
```

### Output:

```
Alice
Bob
```

### Advantages:

* Type-safe
* No need for casting

---

## 4. Java ArrayList Using `List<Object>`

You can store multiple data types using `Object`, the superclass of all Java classes.

```java
import java.util.*;

public class MixedListExample {
    public static void main(String[] args) {
        List<Object> mixedList = new ArrayList<>();
        mixedList.add("Alice");
        mixedList.add(25);
        mixedList.add(5.7);
        mixedList.add(true);
        mixedList.add(null);

        for (Object item : mixedList) {
            System.out.println("Value: " + item + ", Type: " + 
                (item != null ? item.getClass().getSimpleName() : "null"));
        }
    }
}
```

### Output:

```
Value: Alice, Type: String
Value: 25, Type: Integer
Value: 5.7, Type: Double
Value: true, Type: Boolean
Value: null, Type: null
```

### Disadvantages:

* Requires type checking and casting
* Not type-safe

---

## 5. Type Safety Example (Compile-Time Error)

```java
List<Integer> numbers = new ArrayList<>();
numbers.add(100);
numbers.add("oops");  // Compile-time error!
```

This line will not compile because you can't add a `String` to a `List<Integer>`.

---

## 6. Type Casting in `List<Object>`

```java
Object obj = mixedList.get(1); // Returns 25 (Integer)
int age = (int) obj;           // Must cast manually
System.out.println("Age: " + age);
```

---

## 7. Best Practices

* Use type-specific lists whenever possible.
* Only use `List<Object>` when absolutely necessary (e.g., for generic JSON-like data).
* Avoid casting unless you are sure of the data type.

---

## 8. Summary

| Feature               | `List<String>` | `List<Object>`    |
| --------------------- | -------------- | ----------------- |
| Type Safety           | Yes            | No                |
| Supports Mixed Types  | No             | Yes               |
| Requires Casting      | No             | Yes               |
| Compile-Time Checking | Yes            | No (for contents) |

---

Java supports storing different data types in a list via `List<Object>`, but it is generally better to use type-specific lists for safety, clarity, and better compile-time checks. In contrast, Python lists are naturally flexible and accept any type. Understanding the differences between arrays, lists, and generics across languages helps you choose the right data structure for your needs.
