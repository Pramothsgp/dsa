## Problem Statement

You are tasked with implementing a program that manages a group of customers in a store. The store maintains a waiting list of customers in a singly linked list. A unique integer ID represents each customer.

Write a program that adds customers one by one at the front of the line, removes the first customer from the front, and displays the same.

---

### Example

**Input:**
```
4
10 20 30 40
```

**Output:**
```
30 20 10 
```

**Explanation:**

The linked list is constructed as follows:

- Insert 10: `10 -> nullptr`
- Insert 20: `20 -> 10 -> nullptr`
- Insert 30: `30 -> 20 -> 10 -> nullptr`
- Insert 40: `40 -> 30 -> 20 -> 10 -> nullptr`

Remove the first customer (40):  
`30 -> 20 -> 10 -> nullptr`.  
So `30 20 10` is printed as output.

> **Note:** Array implementations will not be supported.

---

### Input Format

- The first line contains an integer `n`, representing the number of customers in the initial line.
- The following line contains `n` space-separated integer IDs of the customers in the line.

### Output Format

- The output should print space-separated integers of the IDs of customers remaining in the queue after removing the first customer.
- The IDs should be printed in the order they appear in the modified line.

Refer to the sample outputs for the formatting specifications.

---

### Code Constraints

- `2 ≤ n ≤ 10`
- `1 ≤ Customer ID's ≤ 500`

---

### Sample Test Cases

**Input 1:**
```
4
10 20 30 40
```
**Output 1:**
```
30 20 10 
```

**Input 2:**
```
2
5 8
```
**Output 2:**
```
5 
```

---

## Java Implementation

```java
import java.util.*;

// Node class representing each customer in the linked list
class Node<T> {
    T data;
    Node<T> next;
    public Node(T data) {
        this.data = data;
        next = null;
    }
}

// LinkedList class to manage the customer queue
class LinkedList<T> {
    Node<T> head;

    public LinkedList() {
        head = null;
    }

    // Insert a new customer at the front of the list
    private void insert(T data) {
        Node<T> newNode = new Node<>(data);
        newNode.next = head;
        head = newNode;
    }

    // Remove the first customer from the front of the list
    private void deleteFirst() {
        if (head == null) {
            System.out.println("List is empty");
            return;
        }
        head = head.next;
    }

    // Print the IDs of customers in the list
    private void printList() {
        Node<T> cur = head;
        while (cur != null) {
            System.out.print(cur.data + " ");
            cur = cur.next;
        }
    }

    // Main method to execute the program logic
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        LinkedList<Integer> ll = new LinkedList<>();
        for (int i = 0; i < n; i++) {
            ll.insert(sc.nextInt());
        }
        ll.deleteFirst();
        ll.printList();
    }
}
```