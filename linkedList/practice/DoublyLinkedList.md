## Problem Statement

Ravi is building a simple application to manage a doubly linked list of integers. He wants to insert new integers into the list and delete a node at a specific position. After deleting it, he needs to display the updated list.

Write a program to ensure that the task is done by performing insertion, deletion at a given position, and then printing the modified list.

---

### Input Format

- The first line contains an integer `n`, representing the number of elements to be inserted into the list.
- The second line contains `n` space-separated integers, representing the values to insert.
- The third line contains an integer `pos`, representing the position of the node to be deleted from the list.

---

### Output Format

- If the given position is valid, print:  
    `Node at position X with value Y deleted successfully.`
- If the position is invalid, print:  
    `Position X not found in the list.`
- In both cases, print:  
    ```
    Data present in the list:
    ```
    followed by the updated list elements on the next line, space separated.

Refer to the sample output for the formatting specifications.

---

### Code Constraints

- 1 ≤ n ≤ 10
- 1 ≤ data ≤ 10³
- 1 ≤ pos ≤ n

---

### Sample Test Cases

#### Input 1:
```
5
10 20 30 40 50
4
```
#### Output 1:
```
Node at position 4 with value 40 deleted successfully.
Data present in the list:
10 20 30 50 
```

#### Input 2:
```
5
10 52 63 74 85
7
```
#### Output 2:
```
Position 7 not found in the list.
Data present in the list:
10 52 63 74 85 
```

---

## Java Implementation

```java
import java.util.*;

// Node class for doubly linked list
class Node<T> {
        T data;
        Node<T> prev, next;

        // Constructor to initialize node data
        public Node(T data) {
                this.data = data;
                prev = next = null;
        }
}

// Doubly linked list class
class DoublyLinkedList<T> {
        Node<T> head;

        public DoublyLinkedList() {
                head = null;
        }

        // Insert a node at the end of the list
        private void insert(T data) {
                if (head == null) {
                        head = new Node<>(data);
                        return;
                }
                Node<T> cur = head;
                while (cur.next != null) {
                        cur = cur.next;
                }
                cur.next = new Node<>(data);
                cur.next.prev = cur;
        }

        // Delete a node at a given position (1-based index)
        private void deleteAt(int k) {
                if (head == null) {
                        System.out.println("List is empty");
                        return;
                }
                Node<T> cur = head;
                // Traverse to the k-th node
                for (int i = 1; i < k && cur != null; i++) {
                        cur = cur.next;
                }
                if (cur == null) {
                        System.out.printf("Position %d not found in the list.\n", k);
                        return;
                }
                // Adjust pointers to remove the node
                if (cur.prev != null) {
                        cur.prev.next = cur.next;
                } else {
                        head = head.next;
                }
                if (cur.next != null) {
                        cur.next.prev = cur.prev;
                }
                System.out.printf("Node at position %d with value %d deleted successfully.\n", k, cur.data);
                cur = null;
        }

        // Print the current list
        private void printList() {
                if (head == null) {
                        System.out.println("List is empty");
                        return;
                }
                System.out.println("Data present in the list:");
                Node<T> cur = head;
                while (cur != null) {
                        System.out.print(cur.data + " ");
                        cur = cur.next;
                }
                System.out.println();
        }

        // Main method to execute the program
        public static void main(String[] args) {
                Scanner sc = new Scanner(System.in);
                DoublyLinkedList<Integer> dl = new DoublyLinkedList<>();
                int n = sc.nextInt();
                for (int i = 0; i < n; i++) {
                        dl.insert(sc.nextInt());
                }

                int k = sc.nextInt();
                dl.deleteAt(k);
                dl.printList();
        }
}
```