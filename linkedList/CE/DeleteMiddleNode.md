# Delete the Middle Node of a Linked List

You are given the head of a linked list. Delete the middle node and return the head of the modified linked list.

The middle node of a linked list of size `n` is the ⌊n / 2⌋th node from the start using 0-based indexing, where ⌊x⌋ denotes the largest integer less than or equal to x.

For `n = 1, 2, 3, 4, 5`, the middle nodes are at indices `0, 1, 1, 2, 2`, respectively.

---

## Examples

### Example 1

**Input:**  
`head = [1, 3, 4, 7, 1, 2, 6]`

**Output:**  
`[1, 3, 4, 1, 2, 6]`

**Explanation:**  
The linked list has 7 nodes. The node at index 3 (value 7) is the middle node and is removed.

---

### Example 2

**Input:**  
`head = [1, 2, 3, 4]`

**Output:**  
`[1, 2, 4]`

**Explanation:**  
The linked list has 4 nodes. The node at index 2 (value 3) is the middle node and is removed.

---

### Example 3

**Input:**  
`head = [2, 1]`

**Output:**  
`[2]`

**Explanation:**  
The linked list has 2 nodes. The node at index 1 (value 1) is the middle node and is removed.

---

## Input Format

- The input consists of a space-separated list of integers representing the values of the linked list nodes.

## Output Format

- The output prints a space-separated list of integers representing the linked list after deleting the middle node.

Refer to the sample output for formatting specifications.

---

## Code Constraints

- `1 ≤ Number of nodes ≤ 20`
- `1 ≤ Node values ≤ 10^3`
- Use 0-based indexing to determine the middle node (⌊n/2⌋).

---

## Sample Test Cases

```
Input 1:
1 3 4 7 1 2 6
Output 1:
1 3 4 1 2 6

Input 2:
1 2 3 4
Output 2:
1 2 4

Input 3:
2 1
Output 3:
2
```

---

## Java Implementation

```java
import java.util.*;

// Node class representing a single node in the linked list
class Node<T> {
    T data;
    Node next;

    public Node(T data) {
        this.data = data;
        next = null;
    }
}

// LinkedList class with methods to insert, print, and delete the middle node
class LinkedList {
    Node<Integer> head = null;

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        LinkedList ll = new LinkedList();
        String[] nums = sc.nextLine().split(" ");
        for (String num : nums) {
            ll.insert(Integer.parseInt(num));
        }
        ll.deleteMiddle();
        ll.print();
    }

    // Insert a new node at the end of the list
    private void insert(int data) {
        if (head == null) {
            head = new Node<>(data);
            return;
        }
        Node cur = head;
        while (cur.next != null) {
            cur = cur.next;
        }
        cur.next = new Node<>(data);
    }

    // Print the linked list
    private void print() {
        Node cur = this.head;
        while (cur != null) {
            System.out.printf("%d ", cur.data);
            cur = cur.next;
        }
    }

    // Delete the middle node using the slow and fast pointer approach
    private void deleteMiddle() {
        // If the list has only one node, remove it
        if (head == null || head.next == null) {
            head = null;
            return;
        }
        // Use two pointers to find the node before the middle node
        Node slow = head;
        Node fast = head.next.next;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        // Remove the middle node
        slow.next = slow.next.next;
    }
}
```