### Recursion: Binary Search with Explanation

#### What is Recursion?

Recursion is a programming technique where a method calls itself to solve a smaller subproblem of the original problem. A recursive function typically has:

* **Base case(s)** to stop recursion
* **Recursive call(s)** to continue reducing the problem

#### Types of Recursion:

* **Linear Recursion**: Each call makes one recursive call (e.g., factorial).
* **Binary Recursion**: Each call makes two recursive calls (e.g., Fibonacci, divide-and-conquer algorithms).
* **Multiple Recursion**: More than two recursive calls (e.g., tree traversal, puzzle solving).

#### What is Binary Search?

Binary Search is an efficient algorithm used to find the position of a target element in a **sorted** array.

* It divides the search interval in half at each step.
* Compares the target with the middle element.
* Recursively searches in the left or right subarray depending on the comparison.

#### How Binary Search Works (Recursively):

1. Compare the target with the middle element.
2. If equal, return the index.
3. If the target is less than the middle, search the left half.
4. If greater, search the right half.
5. Repeat until the subarray size becomes zero (base case).

#### Time and Space Complexity:

* **Time Complexity**: O(log n)

  * At each step, the search space is halved.
* **Space Complexity**: O(log n) for recursive version (due to call stack), O(1) for iterative version.

---

### Java Code: Recursive Binary Search

```java
public class BinarySearchRecursive {

    // Recursive method
    public static int binarySearch(int[] arr, int left, int right, int target) {
        // Base case: if bounds cross, element not found
        if (left > right) {
            return -1;
        }

        int mid = left + (right - left) / 2;

        // Check if the middle element is the target
        if (arr[mid] == target) {
            return mid;
        }

        // If target is smaller, search left half
        if (target < arr[mid]) {
            return binarySearch(arr, left, mid - 1, target);
        }

        // If target is larger, search right half
        return binarySearch(arr, mid + 1, right, target);
    }

    // Main method for testing
    public static void main(String[] args) {
        int[] data = {2, 4, 6, 8, 10, 12, 14};
        int target = 10;

        int result = binarySearch(data, 0, data.length - 1, target);

        if (result != -1) {
            System.out.println("Element found at index: " + result);
        } else {
            System.out.println("Element not found.");
        }
    }
}
```

