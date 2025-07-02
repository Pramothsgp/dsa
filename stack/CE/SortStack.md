## Recursive Stack Sorting (Descending Order)

Write a recursive function that takes an array of integers representing a stack and sorts it **in-place** in descending order (from top to bottom).

### Stack Rules

- The **end of the array** is the **top** of the stack.
- **Allowed operations:**
    - `.pop()` — remove the top element
    - `.append()` — push a new element to the top
    - Access the top element using `arr[-1]`

### Restrictions

- **No loops** or extra data structures (other than the input array).
- **No direct access** to elements inside the array except for the top.
- **Purely recursive** solution.

---

### Input Format

- **First line:** An integer `n` (number of elements in the stack).
- **Second line:** `n` space-separated integers (stack elements from top to bottom).

### Output Format

- A single line containing the sorted stack elements from top to bottom, space-separated.

---

### Code Constraints

- `1 <= n <= 1000`
- `-10^5 <= arr[i] <= 10^5`
- Solution must be **purely recursive**
- Only allowed operations: `.pop()`, `.append()`, and top element access via `arr[-1]` or `arr.get(size - 1)`

---

### Sample Test Cases

#### Input 1
```
5
1 4 3 2 5
```
#### Output 1
```
Sorted stack:
5 4 3 2 1
```

#### Input 2
```
10
10 9 1 2 3 8 7 6 5 4
```
#### Output 2
```
Sorted stack:
10 9 8 7 6 5 4 3 2 1
```

---

## Java Implementation

```java
import java.util.*;

// Custom exception for stack overflow
class StackOverFlowException extends RuntimeException {
        public StackOverFlowException(String msg) {
                super(msg);
        }
}

// Custom exception for empty stack
class EmptyStackException extends RuntimeException {
        public EmptyStackException(String msg) {
                super(msg);
        }
}

// Custom stack implementation with Comparable elements
class CustomStack<T extends Comparable<T>> {
        private T[] datas;
        private int index;

        // Constructor to initialize stack with given size
        public CustomStack(int n) {
                datas = (T[]) new Comparable[n];
                index = -1;
        }

        // Push element to the stack
        public void push(T data) {
                if (isFull()) {
                        throw new StackOverFlowException("Stack is Full");
                }
                datas[++index] = data;
        }

        // Pop element from the stack
        public T pop() {
                if (isEmpty()) {
                        throw new EmptyStackException("Stack is Empty");
                }
                return datas[index--];
        }

        // Peek the top element of the stack
        public T peek() {
                if (isEmpty()) {
                        throw new EmptyStackException("Stack is Empty");
                }
                return datas[index];
        }

        // Check if the stack is empty
        public boolean isEmpty() {
                return index == -1;
        }

        // Check if the stack is full
        public boolean isFull() {
                return index == datas.length - 1;
        }

        // Get the current size of the stack
        public int size() {
                return index + 1;
        }
}

class Solution {
        public static void main(String[] args) {
                Scanner sc = new Scanner(System.in);
                int n = sc.nextInt();
                CustomStack<Integer> stack = new CustomStack<>(n);

                // Push input elements to the stack
                for (int i = 0; i < n; i++) {
                        stack.push(sc.nextInt());
                }

                // Sort the stack recursively
                sortStack(stack);

                System.out.println("Sorted stack:");
                // Print sorted stack elements from top to bottom
                while (!stack.isEmpty()) {
                        System.out.printf("%d ", stack.pop());
                }
        }

        // Recursively sort the stack in descending order
        private static void sortStack(CustomStack<Integer> stack) {
                if (stack.size() <= 1) {
                        return;
                }

                // Remove the top element
                int top = stack.pop();

                // Sort the remaining stack
                sortStack(stack);

                // Insert the removed element in sorted order
                insertInSortedStack(stack, top);
        }

        // Helper function to insert an element into the sorted stack
        private static void insertInSortedStack(CustomStack<Integer> stack, int data) {
                // If stack is empty or top element is less than or equal to data, push data
                if (stack.isEmpty() || stack.peek() <= data) {
                        stack.push(data);
                        return;
                }

                // Otherwise, pop the top and recur
                int top = stack.pop();
                insertInSortedStack(stack, data);

                // Push the top element back after insertion
                stack.push(top);
        }
}
```