
## 🔁 Problem Statement — **Swap Nodes in Pairs**

Given a **singly linked list**, swap every two adjacent nodes and return its head.

⚠️ You **must not modify** the node values. Only the **nodes themselves** may be changed.

---

### 🧾 Input Format:

* A space-separated list of integers representing the node values of a singly linked list.

### 🖨️ Output Format:

* A single line containing a list of integers in square brackets representing the linked list after swapping every two adjacent nodes.

---

### 📌 Constraints:

* The number of nodes in the list is in the range $0, 100$.
* 0 ≤ Node.val ≤ 1000

---

### 🧪 Sample Test Cases:

#### Input 1:

```
1 2 3 4
```

#### Output 1:

```
[2, 1, 4, 3]
```

---

#### Input 2:

```
1
```

#### Output 2:

```
[1]
```

---

#### Input 3:

```
1 2 3
```

#### Output 3:

```
[2, 1, 3]
```

---

## ✅ Java Code

```java
import java.util.*;

class Node {
    int data;
    Node next;

    public Node(int d) {
        data = d;
        next = null;
    }

    public Node(int d, Node next) {
        data = d;
        this.next = next;
    }
}

class LinkedList {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String[] s = sc.nextLine().split("\\s+");

        // Creating linked list from input
        Node head = null, tail = null;
        for (String x : s) {
            if (head == null) {
                head = tail = new Node(Integer.parseInt(x));
            } else {
                tail.next = new Node(Integer.parseInt(x));
                tail = tail.next;
            }
        }

        // Swapping nodes in pairs
        head = swap(head);

        // Collect result into a list
        List<Integer> res = new ArrayList<>();
        tail = head;
        while (tail != null) {
            res.add(tail.data);
            tail = tail.next;
        }

        // Print the result in list format
        System.out.println(res);
    }

    // Function to swap every two adjacent nodes
    private static Node swap(Node head) {
        Node dummy = new Node(0, head);
        Node cur = dummy;

        while (cur.next != null && cur.next.next != null) {
            Node first = cur.next;
            Node second = cur.next.next;

            // Swapping nodes
            first.next = second.next;
            second.next = first;
            cur.next = second;

            // Move to the next pair
            cur = first;
        }

        return dummy.next;
    }
}
```

---
