# Re-arrange Linked List

Given a singly linked list with `n` values, modify the list so that **even numbers** are displayed at the beginning (in reverse order), followed by the **odd numbers** (also in reverse order).

---

## Example

**Input:**
```
5
12 15 13 14 16
```

**Output:**
```
16 14 12 13 15
```

**Explanation:**

- Even numbers: `12, 14, 16` → reversed: `16, 14, 12`
- Odd numbers: `15, 13` → reversed: `13, 15`
- Final list: `16, 14, 12, 13, 15`

---

## Input Format

- The first line contains an integer `n`, the number of elements in the linked list.
- The second line contains `n` space-separated integers, the elements of the linked list.

## Output Format

- Output the modified list: even numbers (reversed), then odd numbers (reversed), space-separated.

---

## Constraints

- `1 ≤ n ≤ 20`
- `1 ≤ elements ≤ 150`

---

## Sample Test Cases

**Input 1:**
```
4
1 2 3 4
```
**Output 1:**
```
4 2 3 1
```

**Input 2:**
```
5
12 15 13 14 16
```
**Output 2:**
```
16 14 12 13 15
```

---

## Java Implementation

```java
import java.util.*;

// Node class for singly linked list
class Node<T>{
    T data;
    Node<T> next;
    public Node(T data){
        this.data = data;
        next = null;   
    }
}

// LinkedList class with required methods
class LinkedList<T>{
    Node<T> head;
    public LinkedList(){
        head = null;
    }
    
    // Build the linked list from array
    private void buildList(T[] nums){
        head = new Node<>(nums[0]);
        Node<T> cur = head;
        for(int i=1;i<nums.length;i++){
            cur.next = new Node<>(nums[i]);
            cur = cur.next;
        }
    }
    
    // Rearrange the list: even numbers reversed, then odd numbers reversed
    private void rearrangeList(){
        Stack<Node<T>> evenStack = new Stack<>();
        Stack<Node<T>> oddStack = new Stack<>();
        
        Node<T> cur = head;
        // Separate nodes into even and odd stacks
        while(cur != null){
            if((Integer)cur.data % 2 == 0){
                evenStack.push(cur);
            } else {
                oddStack.push(cur);
            }
            cur = cur.next;
        }
        Node<T> dummy = new Node<T>(null);
        cur = dummy;
        // Add even nodes in reverse order
        while(!evenStack.isEmpty()){
            cur.next = evenStack.pop();
            cur = cur.next;
        }
        // Add odd nodes in reverse order
        while(!oddStack.isEmpty()){
            cur.next = oddStack.pop();
            cur = cur.next;
        }
        cur.next = null;
        head = dummy.next;
    }
    
    // Print the linked list
    private void printList(){
        Node<T> cur = head;
        while(cur != null){
            System.out.print(cur.data + " ");
            cur = cur.next;
        }
    }
    
    // Main method: read input, build, rearrange, and print list
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        Integer[] nums = new Integer[n];
        for(int i=0;i<n;i++){
            nums[i] = sc.nextInt();
        }
        LinkedList<Integer> ll = new LinkedList<>();
        ll.buildList(nums);
        ll.rearrangeList();
        ll.printList();
    }
}
```
