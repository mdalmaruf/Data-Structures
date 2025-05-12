# Week 1 – Data Structure: Bag (Array-Based)

Welcome!! This week, we will begin by reviewing core Java programming concepts essential for implementing data structures, and then we will implement our first structure: the **Bag ADT** using an array.

---

## Week 1 Objectives

* Set up a Java development environment using IntelliJ IDEA
* Review Java fundamentals: variables, loops, conditionals, arrays, classes, methods
* Understand the concept of Abstract Data Types (ADTs)
* Implement a simple Bag ADT using a fixed-size array
* Practice class interaction and method calls in Java
* Encounter and solve small logical bugs or "tricks" in Java

---

## 🚀 Step 1: Java Environment Setup

### Install IntelliJ IDEA

* Download IntelliJ IDEA Community Edition: [https://www.jetbrains.com/idea/download/](https://www.jetbrains.com/idea/download/)
* Follow this [IntelliJ installation guide](https://www.jetbrains.com/help/idea/installation-guide.html)
* During setup, install the latest **JDK (Java Development Kit)** if prompted

### Create Your First Project

* Open IntelliJ and click "New Project"
* Choose **Java**, select the JDK
* Name the project `DataStructuresIntro`
* Click **Finish** to open the project workspace

---

## 🔄 Step 2: Review of Java Basics

### Java Program Structure

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, COSC2006!");
    }
}
```

* **main method**: Entry point of any Java application
* **System.out.println()**: Used for printing to console

### Variables and Data Types

```java
int number = 10;
double price = 99.99;
String name = "Java";
boolean isAvailable = true;
```

### Conditionals

```java
int value = 7;
if (value == 7)
    System.out.println("Lucky number 7!");
else
    System.out.println("Try again!");
```

### Loops

```java
for (int i = 0; i < 5; i++) {
    System.out.println("i = " + i);
}
```

### Arrays

```java
String[] fruits = {"Apple", "Banana", "Orange"};
System.out.println(fruits[1]); // Output: Banana
```

### 🧠 Tricky Questions

#### 1. Default values

```java
String[] nums = new String[3];
System.out.println(nums[0]);
```

**Expected Output:**

```
null
```

👉 Uninitialized array elements of reference types in Java are `null` by default.

#### 2. String Comparison Surprise

```java
String a = "Java";
String b = new String("Java");
System.out.println(a == b);
System.out.println(a.equals(b));
```

**Expected Output:**

```
false
true
```

👉 `==` compares references; `.equals()` compares values.

#### 3. Post-Increment Mystery

```java
int x = 5;
int y = x++;
System.out.println("x = " + x);
System.out.println("y = " + y);
```

**Expected Output:**

```
x = 6
y = 5
```

👉 `x++` means "use first, then increment".

#### 4. Array Index Out of Bounds

```java
int[] data = {1, 2, 3};
System.out.println(data[3]);
```

**Expected Output:**

```
ArrayIndexOutOfBoundsException
```

👉 Always check the array length before accessing an index!

---

## 🤖 Step 3: Understanding Abstract Data Types (ADTs)

An **ADT** defines a data structure by its behavior (operations) rather than its implementation. A **Bag** is an ADT that:

* Is unordered
* Allows duplicate elements
* Supports operations like `add`, `remove`, and `getSize`

Use case examples:

* Shopping cart
* Multi-set collections

![ADT Concept](https://tse2.mm.bing.net/th?id=OIP.9z-UE-zOJ31Ts8bJiRpzFwHaED\&pid=Api)

---

## 🛠 Step 4: Implementing Bag ADT (Array-Based)

### Create `Bag.java`

```java
public class Bag {
    private final int MAX_SIZE = 100;
    private String[] items;
    private int size;

    public Bag() {
        items = new String[MAX_SIZE];
        size = 0;
    }

    public void add(String item) {
        if (size < MAX_SIZE) {
            items[size] = item;
            size++;
        } else {
            System.out.println("Bag is full!");
        }
    }

    public void display() {
        System.out.println("Items in the bag:");
        for (int i = 0; i < size; i++) {
            System.out.println("- " + items[i]);
        }
    }

    public int getSize() {
        return size;
    }
}
```

### Create `Main.java`

```java
public class Main {
    public static void main(String[] args) {
        Bag myBag = new Bag();
        myBag.add("Apple");
        myBag.add("Banana");
        myBag.add("Notebook");

        myBag.display();
        System.out.println("Total items: " + myBag.getSize());
    }
}
```

### Expected Output:

```
Items in the bag:
- Apple
- Banana
- Notebook
Total items: 3
```

### 🔍 Tricky Twist

```java
myBag.add(null);
myBag.display();
```

**Expected Output:**

```
Items in the bag:
- Apple
- Banana
- Notebook
- null
```

👉 In Java, `null` is a valid reference, and it will be displayed as "null" string in console. Use `if (item != null)` if you want to skip null entries.

---

## 🔮 Challenge Exercises (Optional)

1. Add a method `boolean contains(String item)` to check if an item is in the bag.
2. Add a method `void remove(String item)` to remove one occurrence of an item.
3. Add a method `void clear()` to empty the bag.
4. Print a warning if an item already exists (just for exploration).

---

## 📃 Practice Tasks (To Be Completed in Class)

* [ ] Install IntelliJ IDEA and create project
* [ ] Implement `Bag.java` and `Main.java`
* [ ] Modify your Bag to store integers instead of Strings
* [ ] Change your Bag to accept any type (generics)
* [ ] Try inserting a `null` and handle it gracefully
* [ ] Print Bag items in reverse order (loop from `size - 1` to `0`)
* [ ] Experiment with String identity vs equality (`==` vs `.equals()`)

---

## Further Reading / Tutorials

* [Java Programming Basics by Oracle](https://docs.oracle.com/javase/tutorial/java/index.html)
* [Understanding Bag ADT in Java](https://www.alexomegapy.com/post/understanding-the-bag-adt-in-java-a-flexible-data-structure)
* [Carrano's Textbook Companion Site](https://www.pearson.com/en-us/subject-catalog/p/data-structures-and-abstractions-with-java/P200000002771/9780134831695)

---

## Summary

* Write simple Java programs with variables, loops, arrays, and methods
* Understand what an ADT is and why it is important
* Implement a simple Bag structure using arrays in Java
* Explore Java's default behavior with `null`, arrays, memory, and identity vs equality

We will explore **linked implementations of Bag** next week!
