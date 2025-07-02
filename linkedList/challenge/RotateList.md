# Problem Statement

Pranav wants to **clockwise rotate a doubly linked list** by a specified number of positions. He needs your help to implement a program to achieve this. Given a doubly linked list and an integer representing the number of positions to rotate, write a program to rotate the list clockwise.

---

## Input Format

- The first line of input consists of an integer `n`, representing the number of elements in the linked list.
- The second line consists of `n` space-separated linked list elements.
- The third line consists of an integer `k`, representing the number of positions to rotate the list.

---

## Output Format

- The output displays the elements of the doubly linked list after rotating it by `k` positions.

Refer to the sample output for the formatting specifications.

---

## Code Constraints

- `1 ≤ n ≤ 30`
- `1 ≤ elements ≤ 1000`
- `k < n`

---

## Sample Test Cases

**Input 1:**
```
5
1 2 3 4 5
1
```
**Output 1:**
```
5 1 2 3 4 
```

**Input 2:**
```
5
10 20 30 40 50
3
```
**Output 2:**
```
30 40 50 10 20 
```

---

## Java Implementation

```java
import java.util.*;

// Node class for the linked list
class Node<T>{
    T data;
    Node<T> next;
    public Node(T data){
        this.data = data;
        next = null;
    }
}

// LinkedList class with rotation logic
class LinkedList<T>{
    Node<T> head;
    
    public LinkedList(){
        head = null;
    }
    public LinkedList(T[] data){
        head = null;
        this.buildList(data);
    }
    
    // Build the linked list from array
    private void buildList(T[] nums){
        Node<T> tail = head;
        for(T num : nums){
            if(head == null){
                head = tail = new Node(num);
            } else{
                tail.next = new Node(num);
                tail = tail.next;
            }
        }
    }
    
    // Rotate the list clockwise by k positions
    private void rotateList(int k){
        int len = this.length();
        k = k % len;
        Node<T> tail = head;
        for(int i=1;i<len - k;i++){
            tail = tail.next;
        }
        
        Node<T> newhead = tail.next;
        tail.next = null;
        tail = newhead;
        while(tail.next != null){
            tail = tail.next;
        }
        tail.next = head;
        head = newhead;
    }
    
    // Get the length of the list
    public int length(){
        Node<T> cur = head;
        int len = 0;
        while(cur != null){
            cur = cur.next;
            len++;
        }
        return len;
    }
    
    // Print the list elements
    public void printList(){
        Node<T> cur = head;
        while(cur != null){
            System.out.print(cur.data + " ");
            cur = cur.next;
        }
    }
    
    // Main method to read input and execute rotation
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        Integer[] nums = new Integer[n];
        for(int i=0;i<n;i++){
            nums[i] = sc.nextInt();
        }
        LinkedList<Integer> ll = new LinkedList<>(nums);
        ll.rotateList(sc.nextInt());
        ll.printList();
    }
}
```