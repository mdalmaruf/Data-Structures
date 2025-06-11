# Simple Queue Implementation in Java - Step by Step Guide

We will build a queue using Java step by step. You will first see how to set up a class, then add variables, then create methods without logic, and finally implement those methods. Each step will be followed by a simple explanation.

---

## Step 1: Create the class

First, we create a class named `QueueOperations`. This class will contain all the logic related to our queue.

```java
public class QueueOperations {

}
```

**Explanation:**
We create a public class named `QueueOperations`. Right now it is empty, but we’ll add variables and methods in the next steps.

---

## Step 2: Add queue variables

Next, we add the necessary variables to manage the queue.

```java
public class QueueOperations {
    int maxSize = 5;               // maximum size of the queue
    int[] queue = new int[maxSize]; // array to hold queue elements
    int front = -1;                // pointer to the front of the queue
    int rear = -1;                 // pointer to the rear of the queue
}
```

**Explanation:**

* `maxSize` defines how many elements our queue can hold.
* `queue` is an array to store queue items.
* `front` and `rear` keep track of the first and last elements in the queue.

---

## Step 3: Add the main method and function declarations

Now we’ll add a `main` method to test our code. We’ll also define `enqueue` and `dequeue` methods (just structure, no logic yet).

```java
public class QueueOperations {
    int maxSize = 5;
    int[] queue = new int[maxSize];
    int front = -1;
    int rear = -1;

    public static void main(String[] args) {
        QueueOperations q = new QueueOperations();
        q.enqueue(10);  // test call
        q.enqueue(20);  // test call
        q.dequeue();    // test call
    }

    public void enqueue(int value) {
        System.out.println("Enqueue called with value: " + value);
    }

    public void dequeue() {
        System.out.println("Dequeue called");
    }
}
```

**Explanation:**

* `main` is where the program starts running.
* We create an object `q` and call the `enqueue` and `dequeue` methods.
* Right now, these methods just print messages.

---

## Step 4: Implement the enqueue method

Now let’s write the full logic for the `enqueue` method.

```java
public void enqueue(int value) {
    if (rear == maxSize - 1) {  // Check if queue is full
        System.out.println("Queue is full. Cannot enqueue.");
        return;
    }
    if (front == -1) {
        front = 0;  // Set front if inserting the first element
    }
    rear++;  // Move rear forward
    queue[rear] = value;  // Store value in queue
    System.out.println("Enqueued: " + value);
}
```

**Explanation:**

* If the queue is full, we print an error and return.
* If it’s the first element, we set `front` to 0.
* We increment `rear` and store the new value.

---

## Step 5: Implement the dequeue method

Now let’s write the logic to remove elements.

```java
public void dequeue() {
    if (front == -1 || front > rear) {  // Check if queue is empty
        System.out.println("Queue is empty. Cannot dequeue.");
        return;
    }
    System.out.println("Dequeued: " + queue[front]);  // Remove and print element
    front++;  // Move front to next position
}
```

**Explanation:**

* If the queue is empty (either never used or all elements removed), we print an error.
* Otherwise, we print and remove the front element.

---

## Step 6: Final Complete Code

Here is the complete working version:

```java
public class QueueOperations {
    int maxSize = 5;
    int[] queue = new int[maxSize];
    int front = -1;
    int rear = -1;

    public static void main(String[] args) {
        QueueOperations q = new QueueOperations();
        q.enqueue(10);
        q.enqueue(20);
        q.enqueue(30);
        q.dequeue();
        q.dequeue();
        q.dequeue();
        q.dequeue();  // One extra dequeue to test empty queue
    }

    public void enqueue(int value) {
        if (rear == maxSize - 1) {
            System.out.println("Queue is full. Cannot enqueue.");
            return;
        }
        if (front == -1) {
            front = 0;
        }
        rear++;
        queue[rear] = value;
        System.out.println("Enqueued: " + value);
    }

    public void dequeue() {
        if (front == -1 || front > rear) {
            System.out.println("Queue is empty. Cannot dequeue.");
            return;
        }
        System.out.println("Dequeued: " + queue[front]);
        front++;
    }
}
```

### Expected Output

```
Enqueued: 10
Enqueued: 20
Enqueued: 30
Dequeued: 10
Dequeued: 20
Dequeued: 30
Queue is empty. Cannot dequeue.
```


