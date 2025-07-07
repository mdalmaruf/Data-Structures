# Java: ADT List and Generics

---

## What Is a List in Java?

A **List** is a linear data structure that stores elements in a specific sequence. Java provides:

* `ArrayList`: backed by an array
* `LinkedList`: backed by linked nodes

### Common List Operations

| Method             | Description                       |
| ------------------ | --------------------------------- |
| `add(item)`        | Adds item to the end              |
| `add(index, item)` | Inserts item at specific position |
| `get(index)`       | Retrieves item at index           |
| `set(index, item)` | Updates item at index             |
| `remove(index)`    | Removes item at index             |
| `contains(item)`   | Checks if item exists             |
| `size()`           | Returns number of elements        |

### ArrayList vs LinkedList (Quick Comparison)

| Feature             | ArrayList         | LinkedList        |
| ------------------- | ----------------- | ----------------- |
| Access by index     | ✔ Fast (O(1))     | ✗ Slow (O(n))     |
| Insert/delete start | ✗ Slow (O(n))     | ✔ Fast (O(1))     |
| Insert middle       | ✗ Moderate (O(n)) | ✔ Moderate (O(n)) |
| Memory usage        | ✔ Compact         | ✗ Extra for links |

### Example:

```javajava
List<String> items = new ArrayList<>();
items.add("Pen");
items.add("Notebook");
System.out.println(items.get(0)); // Pen
```

---
## Java Generics (`<T>`)

Generics allow you to write a single class, interface, or method that automatically works with any data type.

### Why It Matters:

* **Type Safety**: Prevents runtime type casting errors
* **Code Reusability**: Same class can be used for `Integer`, `String`, `Vehicle`, etc.
* **Cleaner Code**: No need to cast objects manually

### Generic Syntax in Java:

```java
class MyList<T> { ... }  // T can be any reference type
```

* `T` stands for **Type** (you may also see `E`, `K`, `V` in other contexts)
* When you instantiate the class, Java replaces `T` with your chosen type

### Example Use:

```java
MyList<String> names = new MyList<>(10);
names.add("Alice");
String name = names.get(0);  // No need to cast
```

---

## Custom Generic List Implementation (`MyList<T>`) – Simplified

```java
class MyList<T> {
    private T[] data;
    private int size;

    public MyList(int capacity) {
        data = (T[]) new Object[capacity];
        size = 0;
    }

    public void add(T item) {
        data[size++] = item;
    }

    public T get(int index) {
        return data[index];
    }

    public int size() {
        return size;
    }

    public void printAll() {
        for (int i = 0; i < size; i++) {
            System.out.println(data[i]);
        }
    }
}
```

---

## Vehicle Example with `MyList<Vehicle>`

```java
class Vehicle {
    String name;
    Vehicle(String name) { this.name = name; }
    public void display() {
        System.out.println("Vehicle: " + name);
    }
}

class Car extends Vehicle {
    Car(String name) { super(name); }
    public void display() {
        System.out.println("Car: " + name);
    }
}

class Bike extends Vehicle {
    Bike(String name) { super(name); }
    public void display() {
        System.out.println("Bike: " + name);
    }
}
```

---

## Main Class to Test the List

```java
public class Main {
    public static void main(String[] args) {
        MyList<Vehicle> garage = new MyList<>(5);

        garage.add(new Car("Toyota"));
        garage.add(new Bike("Yamaha"));

        for (int i = 0; i < garage.size(); i++) {
            garage.get(i).display();
        }
    }
}
```

### Output:

```
Car: Toyota
Bike: Yamaha
```


---

## Full Example Code (All Together)

```java
class MyList<T> {
    private T[] data;
    private int size;

    public MyList(int capacity) {
        data = (T[]) new Object[capacity];
        size = 0;
    }

    public void add(T item) {
        data[size++] = item;
    }

    public T get(int index) {
        return data[index];
    }

    public int size() {
        return size;
    }

    public void printAll() {
        for (int i = 0; i < size; i++) {
            System.out.println(data[i]);
        }
    }
}

class Vehicle {
    String name;
    Vehicle(String name) { this.name = name; }
    public void display() {
        System.out.println("Vehicle: " + name);
    }
}

class Car extends Vehicle {
    Car(String name) { super(name); }
    public void display() {
        System.out.println("Car: " + name);
    }
}

class Bike extends Vehicle {
    Bike(String name) { super(name); }
    public void display() {
        System.out.println("Bike: " + name);
    }
}

public class Main {
    public static void main(String[] args) {
        MyList<Vehicle> garage = new MyList<>(5);
        garage.add(new Car("Toyota"));
        garage.add(new Bike("Yamaha"));

        for (int i = 0; i < garage.size(); i++) {
            garage.get(i).display();
        }
    }
}
```

---

## Next Steps:

* Add `remove(index)` method
* Auto-resize when full
* Add `contains()` and `set()` methods

---



