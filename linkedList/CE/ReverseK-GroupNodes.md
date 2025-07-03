# Reverse Nodes in k-Group (Linked List)

Given the head of a linked list, reverse the nodes of the list `k` at a time, and return the modified list.

- `k` is a positive integer less than or equal to the length of the linked list.
- If the number of nodes is not a multiple of `k`, then the left-out nodes should, in the end, remain as they are.
- **You may not alter the values in the list's nodes; only the nodes themselves may be changed.**

---

## Example

### Example 1

**Input:**  
head = 1 2 3 4 5 (size = 5), k = 2

**Output:**  
2 1 4 3 5

---

### Example 2

**Input:**  
head = 1 2 3 4 5 (size = 5), k = 3

**Output:**  
3 2 1 4 5

![Reverse Nodes in k-Group Example](https://assets.leetcode.com/uploads/2020/10/03/reverse_ex2.jpg)
---

## Input Format

- The first line contains an integer `n`, the number of nodes in the linked list.
- The second line contains `n` space-separated integers, representing the values of the linked list nodes.
- The third line contains an integer `k`, the number of nodes to reverse at a time.

## Output Format

- The output displays the modified linked list after reversing the nodes in groups of `k` at a time.
- Each node's value should be printed on the same line, space-separated.

Refer to the sample output for the formatting specifications.

---

## Code Constraints

- The number of nodes in the list is `n`.
- `1 ≤ k ≤ n ≤ 5000`
- `0 ≤ Node.val ≤ 1000`

---

## Sample Test Cases

**Input 1:**
```
5
1 2 3 4 5
2
```
**Output 1:**
```
2 1 4 3 5 
```

**Input 2:**
```
5
1 2 3 4 5
3
```
**Output 2:**
```
3 2 1 4 5 
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

// LinkedList class with methods to build, reverse in k-groups, and print the list
class LinkedList<T>{
    Node<T> head;
    public LinkedList(){
        head = null;
    }
    
    // Builds the linked list from an array of values
    private void buildList(T[] nums){
        head = new Node<>(nums[0]);
        Node<T> cur = head;
        for(int i=1;i<nums.length;i++){
            cur.next = new Node<>(nums[i]);
            cur = cur.next;
        }
    }
    
    // Reverses nodes in groups of k
    private void reverseKGroup(int k){
        Node<T> dummy = new Node<T>(null); // Dummy node to simplify edge cases
        dummy.next = head;
        Node<T> prevGroupEnd = dummy;
        
        while(true){
            Node<T> kth = getKthNode(prevGroupEnd , k); // Find the kth node from prevGroupEnd
            if(kth == null){
                break;
            }
            Node<T> groupStart = prevGroupEnd.next;
            Node<T> nextGroup = kth.next;
            
            // Reverse the group
            Node<T> prev = nextGroup;
            Node<T> cur = groupStart;
            
            while(cur != nextGroup){
                Node<T> next = cur.next;
                cur.next = prev;
                prev = cur;
                cur = next;
            }
            
            prevGroupEnd.next = kth;
            prevGroupEnd = groupStart;
        }
        
        head = dummy.next;
    }
    
    // Helper to get the kth node from the given node
    private Node<T> getKthNode(Node<T> node , int k){
        while(k-- > 0 && node != null){
            node = node.next;
        }
        return node;
    }
    
    // Prints the linked list
    private void printList(){
        Node<T> cur = head;
        while(cur != null){
            System.out.print(cur.data + " ");
            cur = cur.next;
        }
    }
    
    // Main method to read input, process, and print output
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        LinkedList<Integer> ll = new LinkedList<>();
        int n = sc.nextInt();
        Integer[] nums = new Integer[n];
        for(int i=0;i<n;i++){
            nums[i] = sc.nextInt();
        }
        int k = sc.nextInt();
        ll.buildList(nums);
        ll.reverseKGroup(k);
        ll.printList();
    }
}
```