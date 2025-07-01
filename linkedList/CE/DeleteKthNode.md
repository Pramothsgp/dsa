# Remove Nth Node From End of List

Given the head of a linked list, remove the nth node from the end of the list and return its head.

---

## Examples

**Example 1:**

- **Input:** `head = [1,2,3,4,5]`, `n = 2`
- **Output:** `[1,2,3,5]`

**Example 2:**

- **Input:** `head = [1]`, `n = 1`
- **Output:** `[]`

**Example 3:**

- **Input:** `head = [1,2]`, `n = 1`
- **Output:** `[1]`

---

## Input Format

- The first line contains space-separated integers representing the values of the linked list nodes.
- The second line contains a single integer `n`, representing the position (from the end) of the node to remove.

## Output Format

- The output prints a single line containing a list of integers representing the updated linked list after removing the specified node.

Refer to the sample output for the formatting specifications.

---

## Constraints

- `1 ≤ sz ≤ 10`
- `0 ≤ Node.val ≤ 10^3`
- `1 ≤ n ≤ sz`

---

## Sample Test Cases

**Input 1:**
```
1 2 3 4 5
2
```
**Output 1:**
```
[1, 2, 3, 5]
```

**Input 2:**
```
1
1
```
**Output 2:**
```
[]
```

**Input 3:**
```
1 2
1
```
**Output 3:**
```
[1]
```

---

## Java Implementation

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

// LinkedList class with insert, delete, and print methods
class LinkedList<T>{
    Node<T> head = null;
    public LinkedList(){
        head = null;
    }
    
    // Insert a new node at the end of the list
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
    
    // Delete the k-th node from the end of the list
    private void delete(int k){
        if(head == null || head.next == null){
            head = null;
            return;
        }
        delete(head , new int[]{k + 1});
    }

    // Helper recursive function to delete the k-th node from the end
    private void delete(Node<T> node , int[] k){
        if(node == null){
            --k[0];
            return;
        }
        
        delete(node.next , k);
        if(k[0] == 0){
            if(node.next != null){
                node.next = node.next.next;
            }
        }
        --k[0];
    }
    
    // Print the linked list in the required format
    private void print(){
        Node<T> cur = head;
        System.out.printf("[");
        while(cur != null){
            if(cur.next != null){
                System.out.printf("%d, ", cur.data);
            } else{
                System.out.printf("%d", cur.data);
            }
            cur = cur.next;
        }
        System.out.printf("]");
    }

    // Main method to read input, perform deletion, and print result
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        LinkedList<Integer> ll = new LinkedList<>();
        for(String s : sc.nextLine().split(" ")){
            ll.insert(Integer.parseInt(s));
        }
        
        int k = sc.nextInt();
        
        ll.delete(k);
        ll.print();
    }
}
```