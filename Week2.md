# Week 2 – Bag ADT (Linked-Based), Node Class & Chain Operations

Welcome to Week 2! In this lesson, we'll move beyond array-based data structures to explore the power and flexibility of **linked structures**. We'll focus on creating a Bag ADT using a **singly linked list**, implement core operations, and analyze how this model differs from arrays.

---

## Week 2 Objectives

* Understand what a data structure is and its importance
* Learn about Abstract Data Types (ADTs)
* Explore linked lists and dynamic memory
* Implement a Node class
* Build a Bag ADT using a linked chain
* Practice core operations: `add`, `removeFirst`, `display`
* Visualize memory and pointer behavior in Java

---

## 🧩 What Is a Data Structure?

A **data structure** is a specialized format for organizing, processing, retrieving, and storing data. Choosing the right data structure improves efficiency and scalability.

### 📊 Types of Data Structures

| Type       | Examples                  | Common Operations          |
| ---------- | ------------------------- | -------------------------- |
| Linear     | Array, Linked List        | Add, Delete, Traverse      |
| Non-linear | Tree, Graph               | Search, Traverse, Connect  |
| Dynamic    | Linked List, Stack, Queue | Grow/Shrink at runtime     |
| Static     | Array                     | Fixed size at compile-time |

### 💡 Why Use Data Structures?

* To manage large amounts of data efficiently
* To improve code clarity, scalability, and performance
* To solve real-world problems like routing, searching, sorting, and task scheduling

### 🧠 Common Java Terminology (Clarified)

* **Class**: A blueprint or template for creating objects. It defines what properties (fields) and behaviors (methods) an object will have.
* **Object**: A specific instance of a class. Think of it like a cookie made from the cookie-cutter (class).
* **Accessor Method**: A method used to read the value of a private variable. Example: `getSize()` returns the size.
* **Dot Notation (`.`)**: Used in Java to access methods and variables. For example, `bag.getSize()` calls the `getSize()` method of the `bag` object.
* **Arrow Notation (`->`)**: Used in languages like C/C++ to access members via pointers. Java doesn’t use this because everything is passed by reference using objects.

A **data structure** is a way of organizing and storing data to perform operations like insertion, deletion, traversal, and searching efficiently.

### Examples:

* **Arrays** – Fixed size, index-based access
* **Linked Lists** – Dynamically growable, node-based
* **Stacks, Queues, Trees, Graphs** – Specialized access patterns

**Why learn data structures?**

* They're the backbone of all software applications
* Efficient data storage and access = better performance

---

## 🧠 What Is an Abstract Data Type (ADT)?

An **Abstract Data Type (ADT)** is a theoretical concept used in computer science to describe the behavior of data types in terms of the operations they support, without specifying their implementation.

### 🎯 Purpose of ADT

* To **focus on what a data structure does**, not how it is done
* To **hide the internal implementation details** and allow flexibility
* To provide a consistent interface for manipulating data

### 💡 Why Use ADTs?

* Promote **modularity** and **code reuse**
* Help in designing **robust APIs** and interfaces
* Allow programmers to change the implementation without affecting users

### 🧰 Types of Common ADTs and Examples:

| ADT   | Description                                | Common Operations                 | Example Structures            |
| ----- | ------------------------------------------ | --------------------------------- | ----------------------------- |
| List  | Ordered collection with duplicates allowed | Add, remove, traverse             | ArrayList, LinkedList         |
| Stack | LIFO structure                             | push, pop, peek                   | Browser history, undo feature |
| Queue | FIFO structure                             | enqueue, dequeue, peek            | Printer queue, task scheduler |
| Deque | Double-ended queue                         | addFirst, addLast, removeFirst... | LinkedList as deque           |
| Set   | Unordered collection of unique items       | add, remove, contains             | HashSet, TreeSet              |
| Map   | Key-value pairs                            | put, get, remove                  | HashMap, TreeMap              |
| Bag   | Unordered collection allowing duplicates   | add, remove, getFrequency         | Shopping cart                 |

---

## 🧠 Abstract Data Type (ADT) – Bag

A **Bag** is an ADT that:

* Is **unordered**
* Allows **duplicates**
* Supports operations: `add(item)`, `remove(item)`, `getSize()`

Use Case: A Bag can be used to model a shopping cart, or a list of logs/events where order is irrelevant.

---

## 📦 What Is an Array?

### 🧰 Types of Arrays

* **Single-dimensional Array**: Basic list of elements

```java
int[] arr = {1, 2, 3};
System.out.println(arr[0]); // Output: 1
```

* **Multi-dimensional Array**: Array of arrays (e.g., matrix)

```java
int[][] matrix = {
  {1, 2},
  {3, 4}
};
System.out.println(matrix[1][1]); // Output: 4
```

* **Jagged Array**: Array with rows of different lengths

```java
int[][] jagged = new int[2][];
jagged[0] = new int[] {1, 2};
jagged[1] = new int[] {3, 4, 5};
System.out.println(jagged[1][2]); // Output: 5
```

An **array** is a fixed-size, indexed collection of elements stored in contiguous memory locations. Arrays are ideal for fast access when the size is known in advance.

### ✅ Key Characteristics:

* **Index-based access**: Elements accessed via `arr[i]`
* **Fixed size**: Must define length at creation
* **Same data type**: Homogeneous elements

### 🔤 Java Example:

```java
String[] fruits = {"Apple", "Banana", "Mango"};
System.out.println(fruits[1]);
```

**Output:**

```
Banana
```

### 🔁 Common Array Operations:

```java
int[] numbers = new int[5];
numbers[0] = 10;
numbers[1] = 20;
// Update
numbers[0] = 15;
// Delete (manual shift required)
numbers[1] = numbers[2];
```

**Problem:**

* Insertion and deletion are costly (elements must shift)

---

## 🔗 What Is a Chain (Linked List)?

### 🧰 Types of Linked Lists

* **Singly Linked List**: Each node points to the next node only.

```java
Node a = new Node("A");
Node b = new Node("B");
a.next = b;  // A -> B
```

* **Doubly Linked List**: Each node points to both previous and next nodes.

```java
class DNode {
    String data;
    DNode prev, next;
    DNode(String data) { this.data = data; }
}
```

* **Circular Linked List**: The last node points back to the head.

```java
Node head = new Node("X");
head.next = new Node("Y");
head.next.next = head;  // Circular
```

**Example Use Cases:**

* Singly: Simple dynamic stacks
* Doubly: Undo-redo buffers in editors
* Circular: Round-robin scheduling

### 🧰 Types of Linked Lists

* **Singly Linked List**: Each node points to the next node only.
* **Doubly Linked List**: Each node points to both previous and next nodes.
* **Circular Linked List**: The last node points back to the head.

**Example Use Cases:**

* Singly: Simple dynamic stacks
* Doubly: Undo-redo buffers in editors
* Circular: Round-robin scheduling

A **chain** refers to a sequence of **nodes**, each pointing to the next. This structure is the foundation of a **linked list**.

### 📎 What Is a Linked List?

A **linked list** is a linear collection of nodes where each node contains:

* A **data field** storing the value
* A **reference (pointer)** to the next node in the list

### 📌 Example Chain in Memory:

```text
["A"] -> ["B"] -> ["C"] -> null
```

### 🧮 Code to Create a Chain:

```java
Node a = new Node("A");
Node b = new Node("B");
a.next = b;
Node c = new Node("C");
b.next = c;
```

### 📤 Traversing a Chain:

```java
Node current = a;
while (current != null) {
    System.out.println(current.data);
    current = current.next;
}
```

**Output:**

```
A
B
C
```

### 🚀 When to Use Linked Lists?

* When frequent insertion and deletion is required
* When memory usage must grow dynamically
* When array resizing is expensive or wasteful

---

## 🔁 Limitations of Arrays

Arrays:

* Are fixed in size (must predefine capacity)
* Require shifting elements for insertion/deletion
* Waste memory if sparsely filled

| Feature           | Array                       | Linked List                 |
| ----------------- | --------------------------- | --------------------------- |
| Memory            | Contiguous                  | Scattered (dynamic)         |
| Insert/Delete Mid | Costly (shift elements)     | Efficient (update pointers) |
| Random Access     | Fast (O(1))                 | Slow (O(n))                 |
| Resize            | Copy to larger array needed | Grows on demand             |

---

## 🧱 What Is a Linked List?

A **linked list** is a chain of nodes. Each **node** contains:

* A **data** field (value)
* A **next** field (reference to the next node)

### Visual Example:

```
["Apple"] -> ["Banana"] -> ["Notebook"] -> null
```

---

## 💻 Node.java – Creating Node Class

### 🧪 How to Write a Class and Create an Object (for Beginners)

A **class** defines a template for data (fields) and behaviors (methods).
An **object** is a specific instance of that class.

### 📌 Let's Start with a Simple Example:

```java
// A class to represent a Student
public class Student {
    String name;
    int id;

    // Constructor to initialize fields
    public Student(String name, int id) {
        this.name = name;
        this.id = id;
    }

    // Method to display student info
    public void display() {
        System.out.println("Name: " + name + ", ID: " + id);
    }
}
```

### 📦 Creating an Object of the Class:

```java
public class Main {
    public static void main(String[] args) {
        Student s1 = new Student("Alice", 101); // Create object
        s1.display();                            // Call method
    }
}
```

### 🧾 Output:

```
Name: Alice, ID: 101
```

---

Now that you understand classes and objects, creating a `Node` object becomes easier!

```java
// A simple class to represent a node in the linked list
public class Node {
    String data; // Holds the value
    Node next;   // Points to the next node

    public Node(String data) {
        this.data = data;
        this.next = null;
    }
}
```

**Explanation:**

* Every time you create a Node, it can store a value and link to the next one.
* The `next` field is `null` by default, which makes this the tail node.

---

## 🔗 Creating a Chain of Nodes

```java
Node first = new Node("Apple");
Node second = new Node("Banana");
first.next = second;

Node third = new Node("Notebook");
second.next = third;
```

**What happens here?**

* Three nodes are created.
* Each node connects to the next one.
* This forms a chain in memory. You can start from `first` and access all others.

---

## 🧺 LinkedBag.java – Bag Implementation with Links

```java
public class LinkedBag {
    private Node first;
    private int size;

    public LinkedBag() {
        first = null;
        size = 0;
    }

    // Adds an item at the beginning (head)
    public void add(String item) {
        Node newNode = new Node(item);
        newNode.next = first; // Point new node to the former head
        first = newNode;      // Make the new node the head
        size++;
    }

    public void display() {
        Node current = first;
        System.out.println("Bag contains:");
        while (current != null) {
            System.out.println("- " + current.data);
            current = current.next;
        }
    }

    public int getSize() {
        return size;
    }
}
```

**Scenarios:**

* If `add()` is called repeatedly, the most recent item appears first.
* This is a **Last In, First Out** structure in display order.

---

## 🧹 Removing the First Node

```java
// Removes the head node (if exists)
public void removeFirst() {
    if (first != null) {
        first = first.next;
        size--;
    } else {
        System.out.println("Bag is already empty.");
    }
}
```

**What happens if the list is empty?**

* Without a null check, it can throw a `NullPointerException`
* The code above handles this by checking `if (first != null)`

---

## 🧪 Demo: Using LinkedBag

```java
public class Main {
    public static void main(String[] args) {
        LinkedBag myBag = new LinkedBag();
        myBag.add("Apple");
        myBag.add("Banana");
        myBag.add("Notebook");

        myBag.display();

        myBag.removeFirst();
        System.out.println("After removing first:");
        myBag.display();
    }
}
```

**Expected Output:**

```
Bag contains:
- Notebook
- Banana
- Apple
After removing first:
Bag contains:
- Banana
- Apple
```

---

## 🔍 Challenge Functions (Optional but Recommended)

### `boolean contains(String item)`

```java
// Checks if the item exists in the bag
public boolean contains(String item) {
    Node current = first;
    while (current != null) {
        if (current.data.equals(item)) return true;
        current = current.next;
    }
    return false;
}
```

### `void clear()`

```java
// Deletes all nodes by dropping the reference to head
public void clear() {
    first = null;
    size = 0;
    System.out.println("Bag has been cleared.");
}
```

---

## 💬 Discussion Questions

* What trade-offs do you see between arrays and linked lists?
* What happens if we call `removeFirst()` on an empty Bag?
* How might you implement `remove(String item)`?
* Can we traverse the list in reverse?
* How would memory usage compare in a real-time system?

---

## 🔄 More Scenarios, Examples, and Code Explanation

### 🧪 Example: Adding Null Elements

```java
myBag.add(null);  // Allowed in Java, but be cautious
```

**Explanation:**

* Java allows `null` as a value in an object array or linked list
* But it can cause `NullPointerException` during `equals()` or printing
* Best practice: Avoid adding null or add null checks in `add()`

### ❓ What if We Add the Same Item Twice?

```java
myBag.add("Apple");
myBag.add("Apple");
```

**Output:**

```
Bag contains:
- Apple
- Apple
```

✅ A Bag allows duplicates. This behavior is intentional and aligned with the definition of a Bag ADT.

### 🧪 Custom Method: Count Occurrences

```java
public int countOccurrences(String item) {
    int count = 0;
    Node current = first;
    while (current != null) {
        if (current.data != null && current.data.equals(item)) {
            count++;
        }
        current = current.next;
    }
    return count;
}
```

**Usage:**

```java
System.out.println("Count: " + myBag.countOccurrences("Apple"));
```

### 🔁 Reversing the List (Printing Only)

```java
public void displayReverse(Node node) {
    if (node == null) return;
    displayReverse(node.next);
    System.out.println("- " + node.data);
}

public void displayReverse() {
    displayReverse(first);
}
```

**Explanation:** Uses recursion to print items in reverse without changing structure

### ❌ What if We Remove Too Many Times?

```java
myBag.removeFirst();
myBag.removeFirst();
myBag.removeFirst();
myBag.removeFirst();  // List may be empty now
```

**Solution:** `removeFirst()` already checks if `first == null` before proceeding, so it handles this gracefully.

### 🚫 Removing Specific Items

Challenge: Implement `remove(String item)`

```java
public boolean remove(String item) {
    if (first == null) return false;

    if (first.data.equals(item)) {
        first = first.next;
        size--;
        return true;
    }

    Node current = first;
    while (current.next != null) {
        if (current.next.data.equals(item)) {
            current.next = current.next.next;
            size--;
            return true;
        }
        current = current.next;
    }
    return false;
}
```

**Scenario:**

* Removes the first match of the item
* Does nothing if item doesn't exist

---

## 📘 Recap and Concepts

| Concept        | Description                    |
| -------------- | ------------------------------ |
| Node           | Container for data + reference |
| Head           | Start of list                  |
| Tail           | Last node (points to null)     |
| Chain          | Series of linked nodes         |
| Dynamic Growth | Size expands with each node    |

---

## 📚 Recommended Reading

* Goodrich et al., Chapter 3 – Arrays & Linked Lists
* [Visual Linked List Tool](https://visualgo.net/en/list)
* [GeeksForGeeks – Singly Linked List](https://www.geeksforgeeks.org/data-structures/linked-list/)

---

## Summary

* Linked lists solve array size/shift limitations
* Nodes dynamically build flexible memory structures
* Bag ADT can be implemented using a singly linked list
* Java garbage collector cleans up unused nodes
* You practiced key operations: `add`, `removeFirst`, `display`, `contains`, `clear`
