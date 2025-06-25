# Queue Implementation - Print Job Queue

A **Print Job Queue** is a real-world scenario where print jobs are handled in the order they arrive — also known as **First-In-First-Out (FIFO)** order. This tutorial shows you how to build a simple queue system in Java using:
![QueueConcept](images\Queue1.PNG)
1. An **Array-based Queue**
2. A **Linked List-based Queue**

We will walk through the implementation step-by-step.

![QueueExample](images\Queue2.PNG)

## Part A: Queue Using Array in Java (Step-by-Step)

### Step 1: Define the Class
```java
class PrintQueueArray {
    private static final int MAX = 5; // Set a fixed capacity
    private String[] queue;           // Store jobs
    private int front, rear;          // Track positions

    public PrintQueueArray() {
        queue = new String[MAX];
        front = 0;
        rear = 0;
    }
```
**Explanation:**
- `MAX` is the maximum number of jobs the queue can hold.
- `queue` is an array to store job names.
- `front` and `rear` track the current front and next insertion position.

---

### Step 2: Enqueue Method
```java
    public void enqueue(String job) {
        if (rear == MAX) {
            System.out.println("Queue is full. Cannot add job: " + job);
            return;
        }
        queue[rear++] = job;
        System.out.println("Enqueued: " + job);
    }
```
**Explanation:**
- Adds a new job at the `rear` index.
- Increments `rear` after insertion.

---

### 🗑️ Step 3: Dequeue Method
```java
    public String dequeue() {
        if (isEmpty()) {
            System.out.println("Queue is empty. No job to dequeue.");
            return null;
        }
        String job = queue[front++];
        System.out.println("Dequeued: " + job);
        return job;
    }
```
**Explanation:**
- Removes the job at `front`, then moves `front` forward.

---

### 👀 Step 4: Peek & isEmpty
```java
    public String peek() {
        if (isEmpty()) {
            System.out.println("Queue is empty.");
            return null;
        }
        System.out.println("Next job: " + queue[front]);
        return queue[front];
    }

    public boolean isEmpty() {
        return front == rear;
    }
}
```

---

### Step 5: Main Method
```java
public class MainArray {
    public static void main(String[] args) {
        PrintQueueArray queue = new PrintQueueArray();
        queue.enqueue("Job1");
        queue.enqueue("Job2");
        queue.peek();
        queue.dequeue();
        queue.dequeue();
        queue.dequeue();
    }
}
```

### ✅ Output:
```
Enqueued: Job1
Enqueued: Job2
Next job: Job1
Dequeued: Job1
Dequeued: Job2
Queue is empty. No job to dequeue.
```

---

## Part B: Queue Using Linked List in Java

### Step 1: Define Node Class
```java
class Node {
    String data;
    Node next;

    public Node(String data) {
        this.data = data;
        this.next = null;
    }
}
```
**Explanation:**
- A simple node holding job data and the pointer to the next node.

---

### 🔧 Step 2: Define PrintQueueLinkedList
```java
class PrintQueueLinkedList {
    private Node front, rear;
```
- `front`: points to the first job
- `rear`: points to the last job

---

### Step 3: Enqueue Method
```java
    public void enqueue(String job) {
        Node newNode = new Node(job);
        if (rear == null) {
            front = rear = newNode;
        } else {
            rear.next = newNode;
            rear = newNode;
        }
        System.out.println("Enqueued: " + job);
    }
```
**Explanation:**
- Adds a new node to the end.
- Handles first-job and subsequent-job logic.

---

### Step 4: Dequeue Method
```java
    public String dequeue() {
        if (isEmpty()) {
            System.out.println("Queue is empty. No job to dequeue.");
            return null;
        }
        String job = front.data;
        front = front.next;
        if (front == null) {
            rear = null;
        }
        System.out.println("Dequeued: " + job);
        return job;
    }
```
**Explanation:**
- Removes the first node and shifts the front.
- If list becomes empty, set `rear = null`.

---

### 👀 Step 5: Peek & isEmpty
```java
    public String peek() {
        if (isEmpty()) {
            System.out.println("Queue is empty.");
            return null;
        }
        System.out.println("Next job: " + front.data);
        return front.data;
    }

    public boolean isEmpty() {
        return front == null;
    }
}
```

---

### ▶️ Step 6: Main Method
```java
public class MainLinked {
    public static void main(String[] args) {
        PrintQueueLinkedList queue = new PrintQueueLinkedList();
        queue.enqueue("Job1");
        queue.enqueue("Job2");
        queue.peek();
        queue.dequeue();
        queue.dequeue();
        queue.dequeue();
    }
}
```

### Output:
```
Enqueued: Job1
Enqueued: Job2
Next job: Job1
Dequeued: Job1
Dequeued: Job2
Queue is empty. No job to dequeue.
```

---

## Summary Table
| Feature | Array Queue | Linked List Queue |
|--------|-------------|-------------------|
| Size | Fixed | Dynamic |
| Operations | Slower dequeue | Fast enqueue/dequeue |
| Use Case | Small, simple tasks | Scalable systems |

---
