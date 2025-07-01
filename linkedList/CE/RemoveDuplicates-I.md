# Remove Duplicates from Sorted Linked List

Given the head of a sorted linked list, delete all duplicates such that each element appears only once. Return the linked list sorted as well.

---

## Example 1

**Input:**
```
3
1 1 2
```
**Output:**
```
1 2
```

---

## Example 2

**Input:**
```
5
1 1 2 3 3
```
**Output:**
```
1 2 3
```

---

## Input Format

- The first line contains an integer `n` representing the number of nodes in the linked list.
- The second line contains `n` space-separated integers — values of the nodes in sorted order.

## Output Format

- The output consists of a single line with the values of the linked list after removing duplicates, printed in order, separated by spaces.
- If the list is empty (`n = 0`), output will be an empty line.

Refer to the sample output for formatting specifications.

---

## Code Constraints

- The number of nodes in the list is in the range `[0, 300]`.
- `-100 <= Node.val <= 100`
- The list is guaranteed to be sorted in ascending order.

---

## Sample Test Cases

| Input | Output |
|-------|--------|
| `4`<br>`1 1 2 3` | `1 2 3` |
| `7`<br>`1 1 2 2 3 4 4` | `1 2 3 4` |
| `12`<br>`0 0 1 1 1 2 3 3 4 5 5 6` | `0 1 2 3 4 5 6` |
| `3`<br>`1 1 2` | `1 2` |
| `5`<br>`1 1 2 3 3` | `1 2 3` |

---

## Java Implementation

### Approach 1: Remove Duplicates from Sorted List

```java
import java.util.*;

// Node class representing each element in the linked list
class Node<T>{
    T data;
    Node<T> next;
    public Node(T data){
        this.data = data;
        next = null;
    }
}

// LinkedList class with methods to insert, remove duplicates, and print
class LinkedList<T> {
    private Node<T> head;
    
    public LinkedList(){
        head = null;
    }
    
    // Insert a new node at the end
    private void insert(T data){
        if(head == null){
            head = new Node<>(data);
            return;
        }
        
        Node<T> cur = head;
        while(cur.next != null){
            cur = cur.next;
        }
        
        cur.next = new Node<>(data);
    }
    
    // Remove duplicates from sorted linked list
    private void removeDuplicates(){
        Node<T> cur = head;
        while(cur != null && cur.next != null){
            if(cur.data.equals(cur.next.data)){
                cur.next = cur.next.next;
            } else {
                cur = cur.next;
            }
        }
    }
    
    // Print the linked list
    private void print(){
        Node<T> cur = head;
        while(cur != null){
            System.out.print(cur.data + " ");
            cur = cur.next;
        }
    }
    
    // Main method to read input and process the list
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        LinkedList<Integer> l = new LinkedList<>();
        for(String s : sc.nextLine().split(" ")){
            l.insert(Integer.parseInt(s));
        }
        
        l.removeDuplicates();
        l.print();
    }
}
```

---

### Approach 2: Remove Duplicates Using a HashSet

```java
import java.util.*;

// Node class representing each element in the linked list
class Node<T>{
    T data;
    Node<T> next;
    public Node(T data){
        this.data = data;
        next = null;
    }
}

// LinkedList class with methods to insert, remove duplicates, and print
class LinkedList<T> {
    Node<T> head;
    public LinkedList(){
        head = null;
    }
    
    // Insert a new node at the end
    private void insert(T data){
        if(head == null){
            head = new Node<>(data);
            return;
        }
        
        Node<T> cur = head;
        while(cur.next != null){
            cur = cur.next;
        }
        
        cur.next = new Node<>(data);
    }
    
    // Remove duplicates using a HashSet
    private void removeDuplicates(){
        Set<T> seen = new HashSet<>();
        Node<T> cur = head;
        Node<T> prev = null;
        
        while(cur != null){
            if(seen.contains(cur.data)){
                prev.next = cur.next;
            } else {
                seen.add(cur.data);
                prev = cur;
            }
            cur = cur.next;
        }
    }
    
    // Print the linked list
    private void print(){
        Node<T> cur = head;
        while(cur != null){
            System.out.printf("%d " , cur.data);
            cur = cur.next;
        }
    }
    
    // Main method to read input and process the list
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        LinkedList<Integer> ll = new LinkedList<>();
        while(sc.hasNext()){
            ll.insert(Integer.parseInt(sc.next()));
        }
        ll.removeDuplicates();
        ll.print();
    }
}
```