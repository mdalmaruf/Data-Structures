# Tutorial: Understanding Array vs Linked List in Java

## Introduction
Arrays and Linked Lists are two fundamental data structures in computer science. Understanding their differences in structure, use cases, and performance is essential for choosing the right one for a given problem.

---

## Array in Java
An **array** is a fixed-size, contiguous block of memory for storing elements of the same type.

### Example Code with Output
```java
public class ArrayExample {
    public static void main(String[] args) {
        int[] array = new int[5];

        // Insertion
        array[0] = 10;
        array[1] = 20;
        array[2] = 30;

        System.out.println("Array before update:");
        for (int i = 0; i < 3; i++) {
            System.out.print(array[i] + " ");
        }

        // Update
        array[1] = 25;
        System.out.println("\nArray after update:");
        for (int i = 0; i < 3; i++) {
            System.out.print(array[i] + " ");
        }

        // Deletion (shifting)
        for (int i = 1; i < 2; i++) {
            array[i] = array[i + 1];
        }
        array[2] = 0; // optional reset

        System.out.println("\nArray after deletion at index 1:");
        for (int i = 0; i < 3; i++) {
            System.out.print(array[i] + " ");
        }
    }
}
```

---

## Linked List in Java
A **Linked List** is a dynamic data structure made up of nodes. Each node contains data and a reference (pointer) to the next node.

### Node Architecture Explained
A node in a singly linked list contains:
- `data` → actual value (e.g., 10)
- `next` → memory address (reference) to the next node

**Example with Hypothetical Memory Address**
```
[10|0x101] -> [20|0x104] -> [30|null]
```
- `10` is stored at some memory location (e.g., 0x100)
- `next` points to the address of the next node (0x104)

### Accessing a Node
- Start from the `head`
- Traverse using `.next` until you reach the target

### Insertion
To insert `15` after `10`:
```java
Node newNode = new Node(15);
newNode.next = head.next;
head.next = newNode;
```
This connects:
```
[10|0x111] -> [15|0x122] -> [20|0x133]
```

### Deletion
To delete `15`, skip its reference:
```java
head.next = head.next.next;
```

### Update
```java
head.next.data = 99; // changes value of second node
```

---

### Types of Linked Lists

#### 1. Singly Linked List
- Each node points to the next
- Traversal only forward

#### 2. Doubly Linked List
```java
class Node {
  int data;
  Node next;
  Node prev;
}
```
- Each node points forward and backward
- Easy to traverse both ways

#### 3. Circular Linked List
- Last node points back to the first node
```java
lastNode.next = head;
```
- Useful for round-robin scheduling

---

### Example Code with Output
```java
class Node {
    int data;
    Node next;

    Node(int data) {
        this.data = data;
    }
}

public class LinkedListExample {
    public static void main(String[] args) {
        Node head = new Node(10);
        head.next = new Node(20);
        head.next.next = new Node(30);

        System.out.println("Linked List before update:");
        printList(head);

        head.next.data = 25;
        System.out.println("Linked List after update:");
        printList(head);

        Node newNode = new Node(15);
        newNode.next = head.next;
        head.next = newNode;
        System.out.println("Linked List after insert:");
        printList(head);

        Node curr = head;
        while (curr.next != null) {
            if (curr.next.data == 25) {
                curr.next = curr.next.next;
                break;
            }
            curr = curr.next;
        }
        System.out.println("Linked List after delete:");
        printList(head);
    }

    public static void printList(Node node) {
        while (node != null) {
            System.out.print(node.data + " -> ");
            node = node.next;
        }
        System.out.println("null");
    }
}
```

---

## Time & Memory Complexity Explained

### Time Complexity
| Operation        | Array         | Linked List    | Why? |
|------------------|---------------|----------------|------|
| Access           | O(1)          | O(n)           | Arrays use indexing; linked lists require traversal |
| Insert at End    | O(1)*         | O(n)           | Array may need resize; linked list needs to find the last node |
| Insert at Start  | O(n)          | O(1)           | Array needs to shift elements; linked list just changes head |
| Delete at Index  | O(n)          | O(n)           | Both need to shift or traverse to the node |

> Tip: Think in terms of "how many steps" — direct access = O(1), step-by-step = O(n)

### Memory Complexity
- **Array**: Efficient only when fully utilized. Memory waste if only partially used.
- **Linked List**: Flexible sizing, but extra memory required for references/pointers

---

## Summary
- Arrays: Fast access, fixed size
- Linked Lists: Flexible size, efficient insert/delete
- Pick based on: known size, need for speed, frequency of update/delete

---

