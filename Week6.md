# Queue and Circular Queue Tutorial

---

## Section 1: Simple Queue (Using Array)

A **queue** is a linear data structure that follows the **FIFO** (First In, First Out) principle. This means the element inserted first will be removed first, just like a queue of people.

### Key Operations:

* `enqueue(value)`: Add an element to the rear of the queue.
* `dequeue()`: Remove an element from the front.
* `peek()`: View the front element without removing.
* `isEmpty()`: Check if the queue is empty.

### Java Implementation:

```java
public class SimpleQueue {
    private int[] queue;
    private int front;
    private int rear;
    private int size;

    // Constructor to initialize the queue with a fixed capacity
    public SimpleQueue(int capacity) {
        queue = new int[capacity];
        front = 0;
        rear = -1;
        size = 0;
    }

    // Add an element to the queue
    public void enqueue(int value) {
        if (size == queue.length) {
            System.out.println("Queue is full. Cannot enqueue.");
            return;
        }
        rear++;
        queue[rear] = value;
        size++;
        System.out.println(value + " enqueued.");
    }

    // Remove an element from the front
    public int dequeue() {
        if (size == 0) {
            System.out.println("Queue is empty. Cannot dequeue.");
            return -1;
        }
        int result = queue[front];
        front++;
        size--;
        System.out.println(result + " dequeued.");
        return result;
    }

    // Peek at the front element
    public int peek() {
        if (size == 0) {
            System.out.println("Queue is empty. Nothing to peek.");
            return -1;
        }
        return queue[front];
    }

    public boolean isEmpty() {
        return size == 0;
    }

    public int getSize() {
        return size;
    }

    // Main method to test the queue
    public static void main(String[] args) {
        SimpleQueue q = new SimpleQueue(5);
        q.enqueue(10);
        q.enqueue(20);
        q.enqueue(30);
        System.out.println("Front element: " + q.peek());
        q.dequeue();
        q.dequeue();
        System.out.println("Queue is empty? " + q.isEmpty());
    }
}
```

### Expected Output:

```
10 enqueued.
20 enqueued.
30 enqueued.
Front element: 10
10 dequeued.
20 dequeued.
Queue is empty? false
```

---

## Section 2: Circular Queue

A **circular queue** is an advanced form of queue where the last position is connected back to the first to make a circle. It uses space efficiently by wrapping around when the end of the array is reached.

### Applications:

* Round-robin scheduling (Operating Systems)
* Streaming media players
* Circular buffers for logging or real-time data

### Java Implementation:

```java
class CircularQueue {
    private int[] queue;
    private int front;
    private int rear;
    private int size;
    private int capacity;

    public CircularQueue(int capacity) {
        this.capacity = capacity;
        queue = new int[capacity];
        front = 0;
        rear = -1;
        size = 0;
    }

    // Add to circular queue
    public void enqueue(int value) {
        if (isFull()) {
            System.out.println("Circular Queue is full. Cannot enqueue.");
            return;
        }
        rear = (rear + 1) % capacity;
        queue[rear] = value;
        size++;
        System.out.println(value + " enqueued to circular queue.");
    }

    // Remove from circular queue
    public int dequeue() {
        if (isEmpty()) {
            System.out.println("Circular Queue is empty. Cannot dequeue.");
            return -1;
        }
        int result = queue[front];
        front = (front + 1) % capacity;
        size--;
        System.out.println(result + " dequeued from circular queue.");
        return result;
    }

    public int peek() {
        if (isEmpty()) {
            System.out.println("Circular Queue is empty. Nothing to peek.");
            return -1;
        }
        return queue[front];
    }

    public boolean isEmpty() {
        return size == 0;
    }

    public boolean isFull() {
        return size == capacity;
    }

    public static void main(String[] args) {
        CircularQueue cq = new CircularQueue(5);
        cq.enqueue(1);
        cq.enqueue(2);
        cq.enqueue(3);
        cq.dequeue();
        cq.enqueue(4);
        cq.enqueue(5);
        cq.enqueue(6);
        System.out.println("Front element: " + cq.peek());
    }
}
```

### Expected Output:

```
1 enqueued to circular queue.
2 enqueued to circular queue.
3 enqueued to circular queue.
1 dequeued from circular queue.
4 enqueued to circular queue.
5 enqueued to circular queue.
6 enqueued to circular queue.
Front element: 2
```

---

## Summary

| Feature    | Simple Queue          | Circular Queue           |
| ---------- | --------------------- | ------------------------ |
| Memory Use | Linear                | Efficient (reuses space) |
| Insertion  | At rear               | At rear (wrapped)        |
| Deletion   | From front            | From front (wrapped)     |
| Use Cases  | Print tasks, requests | OS scheduling, streaming |
