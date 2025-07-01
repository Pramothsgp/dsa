Given the head of a linked list, return the list after sorting it in ascending order.

---

**Input:**  
```
head = 4 2 1 3
```
**Output:**  
```
1 2 3 4
```
---

**Input:**  
```
head = -1 5 3 4 0
```

**Output:**  
```
-1 0 3 4 5
```

---

### Input format
The input is a space-separated list of integers, which represent the values in the linked list.

### Output format
The output is a space-separated list of integers, representing the sorted linked list.

Refer to the sample output for formatting specifications.

---

### Code constraints

- The number of nodes in the list is in the range [0, 5 * 10⁴].
- -10⁵ ≤ Node.val ≤ 10⁵


---
## Java Implementation
```java
import java.util.*;

class LinkedList {
    // Node class represents each element in the linked list
    private static class Node {
        int data;
        Node next;
        public Node(int data) {
            this.data = data;
            next = null;
        }
    }
    
    private Node head;
    
    // Constructor to initialize the linked list
    private LinkedList() {
        this.head = null;
    }
    
    // Sorts the linked list in ascending order
    private void sort() {
        Node cur = head;
        while (cur != null) {
            Node min = cur, next = cur.next;
            while (next != null) {
                if (min.data > next.data) {
                    min = next;
                }
                next = next.next;
            }
            // Swap data between current node and minimum node found
            if (cur.data > min.data) {
                cur.data = min.data ^ cur.data ^ (min.data = cur.data);
            }
            cur = cur.next;
        }
    }
    
    // Prints the linked list elements
    private void print() {
        Node cur = head;
        while (cur != null) {
            System.out.printf("%d ", cur.data);
            cur = cur.next;
        }
    }
    
    // Inserts a new node with the given data at the end of the list
    private void insert(int data) {
        if (head == null) {
            head = new Node(data);
            return;
        }
        Node cur = head;
        while (cur.next != null) {
            cur = cur.next;
        }
        cur.next = new Node(data);
    }
    
    // Main method to read input, sort the list, and print the result
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        LinkedList ll = new LinkedList(); 
        while (sc.hasNext()) {
            ll.insert(Integer.parseInt(sc.next()));
        }
        ll.sort();
        ll.print();
    }
}
```



### ✅ **Generic LinkedList Implementation:**

```java
import java.util.*;

class LinkedList<T extends Comparable<T>> {
    // Generic Node class
    private static class Node<T> {
        T data;
        Node<T> next;

        public Node(T data) {
            this.data = data;
            this.next = null;
        }
    }

    private Node<T> head;

    public LinkedList() {
        this.head = null;
    }

    // Insert at the end
    public void insert(T data) {
        Node<T> newNode = new Node<>(data);
        if (head == null) {
            head = newNode;
            return;
        }
        Node<T> cur = head;
        while (cur.next != null) {
            cur = cur.next;
        }
        cur.next = newNode;
    }

    // Selection sort
    public void sort() {
        Node<T> cur = head;
        while (cur != null) {
            Node<T> min = cur;
            Node<T> next = cur.next;
            while (next != null) {
                if (next.data.compareTo(min.data) < 0) {
                    min = next;
                }
                next = next.next;
            }
            if (min != cur) {
                T temp = cur.data;
                cur.data = min.data;
                min.data = temp;
            }
            cur = cur.next;
        }
    }

    // Print elements
    public void print() {
        Node<T> cur = head;
        while (cur != null) {
            System.out.print(cur.data + " ");
            cur = cur.next;
        }
        System.out.println();
    }

    // Main for Integer input
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        LinkedList<Integer> ll = new LinkedList<>();
        String[] tokens = sc.nextLine().split(" ");
        for (String token : tokens) {
            ll.insert(Integer.parseInt(token));
        }
        ll.sort();
        ll.print();
        sc.close();
    }
}
```
