# Circular Linked List Tutorial in Java

## Introduction
A **Circular Linked List (CLL)** is a linear data structure in which the last node of the list points back to the first node instead of `null`. This creates a circle of nodes. Circular linked lists are especially useful in situations where the data structure needs to continuously loop over elements like in **round-robin scheduling**, **real-time systems**, **multiplayer games**, and **streaming buffers**.

---

## Why Use a Circular Linked List?
- **Efficient looped traversal**: You can keep cycling through elements.
- **No need to reset to head**: Since last node links to first, looping is natural.
- **Memory efficient**: No dummy head/tail structures needed.

---

## Structure of a Node
Each node has:
- `data`: value stored in the node
- `next`: reference to the next node in the list

```java
class Node {
    int data;
    Node next;

    public Node(int data) {
        this.data = data;
        this.next = null;
    }
}
```

---

## Step-by-Step: Building a Circular Linked List

### Step 1: Create the CircularLinkedList class
We define two pointers:
- `head`: the first node of the list
- `tail`: the last node (whose `next` points to head)

```java
class CircularLinkedList {
    private Node head;
    private Node tail;

    public CircularLinkedList() {
        head = null;
        tail = null;
    }
}
```

---

### Step 2: Insertion at the End
Add a node at the end and point it back to the head.

```java
    public void insert(int data) {
        Node newNode = new Node(data);
        if (head == null) {
            head = newNode;
            tail = newNode;
            tail.next = head;
        } else {
            tail.next = newNode;
            newNode.next = head;
            tail = newNode;
        }
    }
```

**Example**:
```java
list.insert(10);
list.insert(20);
list.insert(30);
```
**Result**: 10 -> 20 -> 30 -> (back to 10)

---

### Step 3: Insertion at the Beginning
Insert a node before the head and update the tail's pointer.

```java
    public void insertAtBeginning(int data) {
        Node newNode = new Node(data);
        if (head == null) {
            head = newNode;
            tail = newNode;
            newNode.next = head;
        } else {
            newNode.next = head;
            head = newNode;
            tail.next = head;
        }
    }
```

---

### Step 4: Deletion at the Beginning
Remove the head node and update tail's `next` to new head.

```java
    public void deleteAtBeginning() {
        if (head == null) return;
        if (head == tail) {
            head = null;
            tail = null;
        } else {
            head = head.next;
            tail.next = head;
        }
    }
```

---

### Step 5: Deletion at the End
Find the second-last node and update tail.

```java
    public void deleteAtEnd() {
        if (head == null) return;
        if (head == tail) {
            head = null;
            tail = null;
        } else {
            Node current = head;
            while (current.next != tail) {
                current = current.next;
            }
            current.next = head;
            tail = current;
        }
    }
```

---

### Step 6: Traverse the List
Go from head to tail and print each node’s data.

```java
    public void printList() {
        if (head == null) {
            System.out.println("List is empty");
            return;
        }
        Node temp = head;
        System.out.print("Circular Linked List: ");
        do {
            System.out.print(temp.data + " ");
            temp = temp.next;
        } while (temp != head);
        System.out.println();
    }
}
```

---

## Running the Demo

```java
public class CircularLinkedListDemo {
    public static void main(String[] args) {
        CircularLinkedList list = new CircularLinkedList();

        System.out.println("Inserting elements at end:");
        list.insert(10);
        list.insert(20);
        list.insert(30);
        list.printList();

        System.out.println("Inserting at beginning:");
        list.insertAtBeginning(5);
        list.printList();

        System.out.println("Deleting from beginning:");
        list.deleteAtBeginning();
        list.printList();

        System.out.println("Deleting from end:");
        list.deleteAtEnd();
        list.printList();
    }
}
```

**Expected Output:**
```
Inserting elements at end:
Circular Linked List: 10 20 30 
Inserting at beginning:
Circular Linked List: 5 10 20 30 
Deleting from beginning:
Circular Linked List: 10 20 30 
Deleting from end:
Circular Linked List: 10 20 
```

---
### Full code
```java
//class name: CircularLinkedListDemo
class Node {
    int data;
    Node next;

    public Node(int data) {
        this.data = data;
        this.next = null;
    }
}

class CircularLinkedList {
    private Node head;
    private Node tail;

    public CircularLinkedList() {
        head = null;
        tail = null;
    }

    public void insert(int data) {
        Node newNode = new Node(data);
        if (head == null) {
            head = newNode;
            tail = newNode;
            tail.next = head;
        } else {
            tail.next = newNode;
            newNode.next = head;
            tail = newNode;
        }
    }

    public void insertAtBeginning(int data) {
        Node newNode = new Node(data);
        if (head == null) {
            head = newNode;
            tail = newNode;
            newNode.next = head;
        } else {
            newNode.next = head;
            head = newNode;
            tail.next = head;
        }
    }

    public void deleteAtBeginning() {
        if (head == null) return;
        if (head == tail) {
            head = null;
            tail = null;
        } else {
            head = head.next;
            tail.next = head;
        }
    }

    public void deleteAtEnd() {
        if (head == null) return;
        if (head == tail) {
            head = null;
            tail = null;
        } else {
            Node current = head;
            while (current.next != tail) {
                current = current.next;
            }
            current.next = head;
            tail = current;
        }
    }

    public void printList() {
        if (head == null) {
            System.out.println("List is empty");
            return;
        }
        Node temp = head;
        System.out.print("Circular Linked List: ");
        do {
            System.out.print(temp.data + " ");
            temp = temp.next;
        } while (temp != head);
        System.out.println();
    }
}

public class CircularLinkedListDemo {
    public static void main(String[] args) {
        CircularLinkedList list = new CircularLinkedList();

        System.out.println("Inserting elements at end:");
        list.insert(10);
        list.insert(20);
        list.insert(30);
        list.printList();

        System.out.println("Inserting at beginning:");
        list.insertAtBeginning(5);
        list.printList();

        System.out.println("Deleting from beginning:");
        list.deleteAtBeginning();
        list.printList();

        System.out.println("Deleting from end:");
        list.deleteAtEnd();
        list.printList();
    }
}

```




## Time Complexity Analysis
| Operation              | Time Complexity |
|------------------------|-----------------|
| Insert at beginning    | O(1)            |
| Insert at end          | O(1)            |
| Delete at beginning    | O(1)            |
| Delete at end          | O(n)            |
| Traverse/Print list    | O(n)            |

---

## Bonus Application: Round-Robin Task Scheduler

### Scenario
Simulate a CPU scheduler using a circular linked list. Each node holds a process name and burst time. The scheduler gives each process a time slice.
### Key Concepts
- **Burst Time**: This is the total execution time (in milliseconds) required by a task or process.
- **Quantum Time**: The fixed time slice (in milliseconds) allocated to each task in one cycle of the round-robin scheduler.

If a task's burst time is more than the quantum, it will be paused and resumed in the next round. If it is equal to or less than the quantum, it completes in that cycle.


### Code
```java
class TaskNode {
    String name;
    int burst;
    TaskNode next;

    public TaskNode(String name, int burst) {
        this.name = name;
        this.burst = burst;
    }
}

class TaskScheduler {
    private TaskNode head = null;
    private TaskNode tail = null;

    public void addTask(String name, int burst) {
        TaskNode newTask = new TaskNode(name, burst);
        if (head == null) {
            head = newTask;
            tail = newTask;
            tail.next = head;
        } else {
            tail.next = newTask;
            newTask.next = head;
            tail = newTask;
        }
    }

    public void runScheduler(int quantum) {
        System.out.println("Running Round Robin Scheduler with quantum = " + quantum);
        TaskNode current = head;
        while (true) {
            boolean done = true;
            TaskNode temp = current;
            do {
                if (temp.burst > 0) {
                    System.out.println("Running task: " + temp.name);
                    int runTime = Math.min(temp.burst, quantum);
                    temp.burst -= runTime;
                    System.out.println("Executed for: " + runTime + "ms, Remaining: " + temp.burst);
                    done = false;
                }
                temp = temp.next;
            } while (temp != current);
            if (done) break;
        }
        System.out.println("All tasks completed.");
    }

    public void printTasks() {
        if (head == null) {
            System.out.println("No tasks.");
            return;
        }
        TaskNode current = head;
        do {
            System.out.println("Task: " + current.name + ", Burst Time: " + current.burst);
            current = current.next;
        } while (current != head);
    }
}

public class RoundRobinDemo {
    public static void main(String[] args) {
        TaskScheduler scheduler = new TaskScheduler();
        scheduler.addTask("P1", 5);
        scheduler.addTask("P2", 8);
        scheduler.addTask("P3", 3);

        scheduler.printTasks();
        scheduler.runScheduler(2);
    }
}
```

### Output (Example)
```
Task: P1, Burst Time: 5
Task: P2, Burst Time: 8
Task: P3, Burst Time: 3
Running Round Robin Scheduler with quantum = 2
Running task: P1
Executed for: 2ms, Remaining: 3
Running task: P2
Executed for: 2ms, Remaining: 6
Running task: P3
Executed for: 2ms, Remaining: 1
... [continues]
All tasks completed.
```

### GUI based Implementation
##### Why Add a GUI?
Adding a graphical interface allows students to interact with the scheduler visually. It improves understanding by allowing real-time observation of tasks being processed.

##### Features
- GUI to input task name and burst time
- Set quantum time and execute the scheduler
- Real-time output in a text area
```java
import javax.swing.*;
import java.awt.*;
import java.awt.event.*;

class GUITask {
    String name;
    int burst;
    GUITask next;

    public GUITask(String name, int burst) {
        this.name = name;
        this.burst = burst;
    }
}

class GUIScheduler {
    private GUITask head = null;
    private GUITask tail = null;

    public void addTask(String name, int burst) {
        GUITask newTask = new GUITask(name, burst);
        if (head == null) {
            head = newTask;
            tail = newTask;
            tail.next = head;
        } else {
            tail.next = newTask;
            newTask.next = head;
            tail = newTask;
        }
    }

    public String run(int quantum) {
        StringBuilder log = new StringBuilder();
        if (head == null) return "No tasks.";
        GUITask current = head;
        while (true) {
            boolean done = true;
            GUITask temp = current;
            do {
                if (temp.burst > 0) {
                    log.append("Running task: " + temp.name + "\n");
                    int runTime = Math.min(temp.burst, quantum);
                    temp.burst -= runTime;
                    log.append("Executed for: " + runTime + "ms, Remaining: " + temp.burst + "\n");
                    done = false;
                }
                temp = temp.next;
            } while (temp != current);
            if (done) break;
        }
        log.append("All tasks completed.\n");
        return log.toString();
    }
}

public class SchedulerGUI {
    public static void main(String[] args) {
        JFrame frame = new JFrame("Round Robin Scheduler");
        frame.setSize(450, 450);
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setLayout(new FlowLayout());

        JTextField taskName = new JTextField(10);
        JTextField burstTime = new JTextField(5);
        JTextField quantumTime = new JTextField(5);
        JButton addBtn = new JButton("Add Task");
        JButton runBtn = new JButton("Run Scheduler");
        JTextArea output = new JTextArea(15, 35);
        output.setEditable(false);

        GUIScheduler scheduler = new GUIScheduler();

        frame.add(new JLabel("Task Name:")); frame.add(taskName);
        frame.add(new JLabel("Burst Time:")); frame.add(burstTime);
        frame.add(addBtn);
        frame.add(new JLabel("Quantum:")); frame.add(quantumTime);
        frame.add(runBtn);
        frame.add(new JScrollPane(output));

        addBtn.addActionListener(e -> {
            String name = taskName.getText();
            int burst = Integer.parseInt(burstTime.getText());
            scheduler.addTask(name, burst);
            output.append("Added Task: " + name + "\n");
        });

        runBtn.addActionListener(e -> {
            int quantum = Integer.parseInt(quantumTime.getText());
            String result = scheduler.run(quantum);
            output.append("\n" + result);
        });

        frame.setVisible(true);
    }
}
```

---

## Summary
- Circular linked lists are useful for problems that require cyclic traversal.
- Round-robin scheduling is one of the most practical applications.
- Easy to implement and highly customizable in Java.

