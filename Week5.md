# Understanding Array vs Linked List  and Stack in Java

## Introduction
Arrays and Linked Lists are two fundamental data structures in computer science. Understanding their differences in structure, use cases, and performance is essential for choosing the right one for a given problem.

---

## Array in Java
An **array** is a fixed-size, contiguous block of memory for storing elements of the same type.

### Static Array
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
### Dynamic Array (ArrayList)
In Java, `ArrayList` is a resizable array from the `java.util` package:
```java
import java.util.ArrayList;

public class DynamicArrayExample {
    public static void main(String[] args) {
        ArrayList<Integer> list = new ArrayList<>();

        // Insertion
        list.add(10);
        list.add(20);
        list.add(30);

        System.out.println("ArrayList before update: " + list);

        // Update
        list.set(1, 25);
        System.out.println("ArrayList after update: " + list);

        // Deletion
        list.remove(1);
        System.out.println("ArrayList after deletion: " + list);
    }
}
```

### Notes on Dynamic Arrays:
- ArrayLists grow automatically by allocating a new larger array when needed
- Internally, they double the capacity when size limit is reached
- Trade-off: resizing takes time (O(n)), but you rarely hit it often

## Linked List in Java
A **Linked List** is a dynamic data structure made up of nodes. Each node contains data and a reference (pointer) to the next node.

### Importance of Linked List
- Dynamic memory allocation: size can grow/shrink as needed
- Efficient insertions/deletions: no need to shift elements like arrays
- Used in real-world scenarios like:
  - Implementing stacks and queues
  - Graph representations (adjacency list)
  - Music playlists, navigation systems, undo/redo functionality
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

### Example
```java
// Node structure for Linked List
class Node {
    int data;       // value stored in node
    Node next;      // reference to the next node

    Node(int data) {
        this.data = data;
    }
}

public class LinkedListExample {
    public static void main(String[] args) {
        // Step 1: Create initial linked list: 10 -> 20 -> 30
        Node head = new Node(10);
        head.next = new Node(20);
        head.next.next = new Node(30);

        // Step 2: Print current list
        Node temp = head;
        System.out.println("Linked List before update:");
        while (temp != null) {
            System.out.print(temp.data + " -> ");
            temp = temp.next;
        }
        System.out.println("null");

        // Step 3: Update node with value 20 to 25
        head.next.data = 25;
        temp = head;
        System.out.println("Linked List after update:");
        while (temp != null) {
            System.out.print(temp.data + " -> ");
            temp = temp.next;
        }
        System.out.println("null");

        // Step 4: Insert 15 after 10 → new list: 10 -> 15 -> 25 -> 30
        Node newNode = new Node(15); // create new node
        newNode.next = head.next;   // point it to 25
        head.next = newNode;        // insert after 10

        temp = head;
        System.out.println("Linked List after insert:");
        while (temp != null) {
            System.out.print(temp.data + " -> ");
            temp = temp.next;
        }
        System.out.println("null");

        // Step 5: Delete node with value 25
        Node current = head;
        while (current.next != null) {
            if (current.next.data == 25) {
                current.next = current.next.next; // skip node with 25
                break;
            }
            current = current.next;
        }

        temp = head;
        System.out.println("Linked List after delete:");
        while (temp != null) {
            System.out.print(temp.data + " -> ");
            temp = temp.next;
        }
        System.out.println("null");
    }
}
```

### Expected Output for Linked List Code:
```
Linked List before update:
10 -> 20 -> 30 -> null
Linked List after update:
10 -> 25 -> 30 -> null
Linked List after insert:
10 -> 15 -> 25 -> 30 -> null
Linked List after delete:
10 -> 15 -> 30 -> null
```

---

#### Alternativel you can use this
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

        /* Node head = new Node(10);
        Node current = head;
        
        // Insert additional nodes using a loop
        int[] values = {20, 30, 40, 50};
        for (int val : values) {
            current.next = new Node(val);
            current = current.next;
        }*/

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


## Stack Implementation using Array
A **Stack** is a linear data structure that follows the **LIFO** (Last In, First Out) principle. The last element inserted is the first one to be removed.

### Core Operations:
- **push(x)** – Add element `x` to the top of the stack
- **pop()** – Remove and return the top element
- **peek()** – View the top element without removing
- **isEmpty()** – Check if the stack has no elements

### Where and Why Do We Use Stacks?
Stacks are used in many applications where **reversing** or **backtracking** is needed:
- **Undo/Redo** operations in text editors
- **Function call management** (call stack in recursion)
- **Expression parsing** (e.g., parentheses matching, postfix evaluation)
- **Browser navigation** (back/forward button)
### Simple Stack in Java using Array (with comments)
```java
public class StackUsingArray {
    private int maxSize;       // Maximum size of the stack
    private int[] stackArray;  // Array to store stack elements
    private int top;           // Index of the top element

    // Constructor to initialize stack
    public StackUsingArray(int size) {
        maxSize = size;
        stackArray = new int[maxSize];
        top = -1; // stack is initially empty
    }

    // Push element to top of stack
    public void push(int value) {
        if (top == maxSize - 1) {
            System.out.println("Stack Overflow"); // can't push, stack is full
        } else {
            stackArray[++top] = value; // increment top and insert
        }
    }

    // Pop element from top of stack
    public int pop() {
        if (top == -1) {
            System.out.println("Stack Underflow"); // can't pop, stack is empty
            return -1;
        } else {
            return stackArray[top--]; // return and then decrement top
        }
    }

    // Peek at the top element without removing
    public int peek() {
        if (top == -1) {
            System.out.println("Stack is Empty");
            return -1;
        } else {
            return stackArray[top];
        }
    }

    // Check if the stack is empty
    public boolean isEmpty() {
        return (top == -1);
    }

    // Main method to test stack functionality
    public static void main(String[] args) {
        StackUsingArray stack = new StackUsingArray(5); // create a stack of size 5

        stack.push(10); // push 10
        stack.push(20); // push 20
        stack.push(30); // push 30

        System.out.println("Top element: " + stack.peek()); // should print 30
        System.out.println("Popped: " + stack.pop()); // should remove 30
        System.out.println("Popped: " + stack.pop()); // should remove 20
        System.out.println("Is stack empty? " + stack.isEmpty()); // false
    }
}
```

---
## Expression Notations and Stack Use

### Types of Notations
- **Infix**: Operators are written between operands.
  - Example: `A + B`
  - Requires parentheses and precedence rules

- **Prefix (Polish Notation)**: Operator before operands.
  - Example: `+ A B`
  - Eliminates need for parentheses but hard to evaluate without recursion or stack

- **Postfix (Reverse Polish Notation)**: Operator after operands.
  - Example: `A B +`
  - Easy to evaluate using a **stack**

### Why Use Stack for Expression Evaluation?
- Stack helps manage operands and operators in the correct order
- It allows evaluating expressions without using precedence rules or parentheses
- Ideal for compilers, interpreters, and calculators

### What is Postfix?
In **Postfix notation** (also known as Reverse Polish Notation), the operator comes **after** the operands. For example:
```
Infix:     2 + 3 * 4
Postfix:   2 3 4 * +
```

### Step-by-Step Stack Logic
To evaluate a postfix expression:
1. **Scan the expression from left to right**
2. If it's a **number**, push it onto the stack
3. If it's an **operator**, pop two elements from the stack, apply the operation, and push the result back
4. Repeat until the end

### Java Implementation
```java
import java.util.Stack;

public class PostfixEvaluator {
    public static int evaluatePostfix(String expr) {
        Stack<Integer> stack = new Stack<>();

        for (String token : expr.split(" ")) {
            if (isNumeric(token)) {
                stack.push(Integer.parseInt(token));
            } else {
                int b = stack.pop();
                int a = stack.pop();
                switch (token) {
                    case "+": stack.push(a + b); break;
                    case "-": stack.push(a - b); break;
                    case "*": stack.push(a * b); break;
                    case "/": stack.push(a / b); break;
                }
            }
        }
        return stack.pop();
    }

    public static boolean isNumeric(String s) {
        try {
            Integer.parseInt(s);
            return true;
        } catch (NumberFormatException e) {
            return false;
        }
    }

    public static void main(String[] args) {
        String postfix = "5 1 2 + 4 * + 3 -";  // (5 + ((1 + 2) * 4)) - 3 = 14
        int result = evaluatePostfix(postfix);
        System.out.println("Result: " + result);
    }
}
```

### 🧾 Expected Output:
```
Result: 14
```
The expression `5 1 2 + 4 * + 3 -` is a postfix form of the infix expression `(5 + ((1 + 2) * 4)) - 3`. Here's how it works step by step using a stack:

| Token | Action                                      | Operands      | Operation Performed   | Result | Stack State      |
|-------|---------------------------------------------|---------------|------------------------|--------|------------------|
| 5     | Push 5                                       |               |                        |        | [5]              |
| 1     | Push 1                                       |               |                        |        | [5, 1]           |
| 2     | Push 2                                       |               |                        |        | [5, 1, 2]        |
| +     | Pop 2, 1 → Push (1 + 2)                      | 1, 2          | 1 + 2                  | 3      | [5, 3]           |
| 4     | Push 4                                       |               |                        |        | [5, 3, 4]        |
| *     | Pop 4, 3 → Push (3 * 4)                      | 3, 4          | 3 * 4                  | 12     | [5, 12]          |
| +     | Pop 12, 5 → Push (5 + 12)                    | 5, 12         | 5 + 12                 | 17     | [17]             |
| 3     | Push 3                                       |               |                        |        | [17, 3]          |
| -     | Pop 3, 17 → Push (17 - 3)                    | 17, 3         | 17 - 3                 | 14     | [14]             |

Final result on top of the stack is **14**.


| Token | Action                                     | Stack State      |
|-------|--------------------------------------------|------------------|
| 5     | Push 5                                      | [5]              |
| 1     | Push 1                                      | [5, 1]           |
| 2     | Push 2                                      | [5, 1, 2]        |
| +     | Pop 2, 1 → Push (1 + 2 = 3)                 | [5, 3]           |
| 4     | Push 4                                      | [5, 3, 4]        |
| *     | Pop 4, 3 → Push (3 * 4 = 12)                | [5, 12]          |
| +     | Pop 12, 5 → Push (5 + 12 = 17)              | [17]             |
| 3     | Push 3                                      | [17, 3]          |
| -     | Pop 3, 17 → Push (17 - 3 = 14)              | [14]             |
```


---

