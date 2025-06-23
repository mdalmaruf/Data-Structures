# Circular & Doubly Linked Queues, Priority Queue Implementation Tutorial in Java

## 📌 Introduction
This tutorial covers three important queue data structures:

1. **Circular Queue using Linked List**
2. **Doubly Linked Queue (Deque)**
3. **Priority Queue using Linked List**

Each data structure includes explanations, Java code, and example outputs to help you understand their behaviors and use-cases.

---

## 🔁 1. Circular Queue Using Linked List
A **Circular Queue** is a queue in which the last position is connected back to the first position to make a circle.

### Key Operations:
- **Enqueue (insert)**: Adds an item at the rear.
- **Dequeue (remove)**: Removes item from the front.
- **Peek**: Returns the front item without removing it.

### Java Implementation
```java
class Node {
    int data;
    Node next;

    public Node(int data) {
        this.data = data;
        this.next = null;
    }
}

class CircularQueue {
    private Node front = null;
    private Node rear = null;

    public void enqueue(int data) {
        Node newNode = new Node(data);
        if (front == null) {
            front = newNode;
            rear = newNode;
            rear.next = front;
        } else {
            rear.next = newNode;
            rear = newNode;
            rear.next = front;
        }
    }

    public void dequeue() {
        if (front == null) {
            System.out.println("Queue is empty");
            return;
        }
        if (front == rear) {
            front = null;
            rear = null;
        } else {
            front = front.next;
            rear.next = front;
        }
    }

    public void display() {
        if (front == null) {
            System.out.println("Queue is empty");
            return;
        }
        Node temp = front;
        do {
            System.out.print(temp.data + " ");
            temp = temp.next;
        } while (temp != front);
        System.out.println();
    }
}
```

### Example Output:
```
Enqueue: 10 20 30
Queue: 10 20 30
Dequeue
Queue: 20 30
```

---

## 🔄 2. Doubly Linked Queue (Deque)
A **Deque** (Double Ended Queue) is a data structure where elements can be inserted or removed from both ends.

### Java Implementation
```java
class DNode {
    int data;
    DNode next, prev;

    public DNode(int data) {
        this.data = data;
    }
}

class Deque {
    private DNode front, rear;

    public void insertFront(int data) {
        DNode newNode = new DNode(data);
        if (front == null) {
            front = rear = newNode;
        } else {
            newNode.next = front;
            front.prev = newNode;
            front = newNode;
        }
    }

    public void insertRear(int data) {
        DNode newNode = new DNode(data);
        if (rear == null) {
            front = rear = newNode;
        } else {
            rear.next = newNode;
            newNode.prev = rear;
            rear = newNode;
        }
    }

    public void deleteFront() {
        if (front == null) return;
        front = front.next;
        if (front != null) front.prev = null;
        else rear = null;
    }

    public void deleteRear() {
        if (rear == null) return;
        rear = rear.prev;
        if (rear != null) rear.next = null;
        else front = null;
    }

    public void display() {
        DNode temp = front;
        while (temp != null) {
            System.out.print(temp.data + " ");
            temp = temp.next;
        }
        System.out.println();
    }
}
```

---

## 🎯 3. Priority Queue Using Linked List
A **Priority Queue** arranges items based on priority rather than insertion order. Here, smaller numbers indicate higher priority.

### Java Implementation
```java
class PQNode {
    int data;
    int priority;
    PQNode next;

    public PQNode(int data, int priority) {
        this.data = data;
        this.priority = priority;
    }
}

class PriorityQueueLL {
    private PQNode head = null;

    public void insert(int data, int priority) {
        PQNode newNode = new PQNode(data, priority);
        if (head == null || priority < head.priority) {
            newNode.next = head;
            head = newNode;
        } else {
            PQNode temp = head;
            while (temp.next != null && temp.next.priority <= priority) {
                temp = temp.next;
            }
            newNode.next = temp.next;
            temp.next = newNode;
        }
    }

    public void delete() {
        if (head == null) {
            System.out.println("Queue is empty");
        } else {
            System.out.println("Deleted: " + head.data);
            head = head.next;
        }
    }

    public void display() {
        PQNode temp = head;
        while (temp != null) {
            System.out.print("[" + temp.data + "|P" + temp.priority + "] -> ");
            temp = temp.next;
        }
        System.out.println("null");
    }
}
```

### Example:
```
Insert: (10, 2), (5, 1), (8, 3)
Queue: [5|P1] -> [10|P2] -> [8|P3] -> null
Delete: 5
Queue: [10|P2] -> [8|P3] -> null
```

---

