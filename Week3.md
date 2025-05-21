# ArrayBag

```python
public class ArrayBag {
    private String[] bag;
    private int size;

    // Constructor to initialize the bag with fixed size
    public ArrayBag(int capacity) {
        bag = new String[capacity];
        size = 0;
    }

    // Add an item to the bag
    public boolean add(String item) {
        if (size >= bag.length) {
            return false; // Bag is full
        }
        bag[size] = item;
        size++;
        return true;
    }

    // Remove one occurrence of the item
    public boolean remove(String item) {
        for (int i = 0; i < size; i++) {
            if (bag[i].equals(item)) {
                bag[i] = bag[size - 1]; // Replace with last item
                bag[size - 1] = null;
                size--;
                return true;
            }
        }
        return false;
    }

    // Check if the bag contains the item
    public boolean contains(String item) {
        for (int i = 0; i < size; i++) {
            if (bag[i].equals(item)) {
                return true;
            }
        }
        return false;
    }

    // Return number of items in the bag
    public int getSize() {
        return size;
    }

    // Check if the bag is empty
    public boolean isEmpty() {
        return size == 0;
    }

    // Display contents of the bag
    public void display() {
        System.out.print("Bag contents: [");
        for (int i = 0; i < size; i++) {
            System.out.print(bag[i]);
            if (i < size - 1) {
                System.out.print(", ");
            }
        }
        System.out.println("]");
    }
}

```

# Main Class
```python
public class Main {
    public static void main(String[] args) {
        ArrayBag arrayBag = new ArrayBag(10);

        System.out.println("=== Testing ArrayBag ===");
        arrayBag.add("Apple");
        arrayBag.add("Banana");
        arrayBag.add("Apple");
        arrayBag.add("Orange");
        arrayBag.add("Grapes");

        arrayBag.display();
        System.out.println("Contains 'Apple'? " + arrayBag.contains("Apple"));
        System.out.println("Removing 'Apple': " + arrayBag.remove("Apple"));
        arrayBag.display();
        System.out.println("Size: " + arrayBag.getSize());
        System.out.println("Is Empty? " + arrayBag.isEmpty());
    }
}

```

# LinkedList Demo

```python
public class LinkedListDemo {

    // Inner Node class
    static class Node {
        String data;
        Node next;

        Node(String data) {
            this.data = data;
            this.next = null;
        }
    }

    // Head of the list
    Node head;

    // Add a new item to the beginning of the list
    public void add(String item) {
        Node newNode = new Node(item);
        newNode.next = head;
        head = newNode;
    }

    // Display all elements
    public void display() {
        Node current = head;
        System.out.print("Linked List: [");
        while (current != null) {
            System.out.print(current.data);
            if (current.next != null) {
                System.out.print(" -> ");
            }
            current = current.next;
        }
        System.out.println("]");
    }

    // Count elements in the list
    public int count() {
        int count = 0;
        Node current = head;
        while (current != null) {
            count++;
            current = current.next;
        }
        return count;
    }

    // Main method for demonstration
    public static void main(String[] args) {
        LinkedListDemo list = new LinkedListDemo();

        list.add("Cat");
        list.add("Dog");
        list.add("Bird");

        list.display(); // Output: Linked List: [Bird -> Dog -> Cat]
        System.out.println("Total nodes: " + list.count()); // Output: 3
    }
}

```
