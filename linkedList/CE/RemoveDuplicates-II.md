
# Remove Duplicates from Sorted List II

Given the head of a sorted linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list. Return the linked list sorted as well.

---

## Example 1

**Input:**  
`head = [1,2,3,3,4,4,5]`

**Output:**  
`[1,2,5]`

---

## Example 2

**Input:**  
`head = [1,1,1,2,3]`

**Output:**  
`[2,3]`

---

## Input Format

- The input consists of a space-separated sequence of integers, representing the sorted linked list values.

## Output Format

- The output prints the values of the resulting linked list after removing all duplicates completely.
- The output is a single line of space-separated integers.

Refer to the sample output for formatting specifications.

---

## Code Constraints

- The number of nodes in the list is in the range `[0, 300]`.
- `-100 <= Node.val <= 100`
- The list is guaranteed to be sorted in ascending order.

---

## Sample Test Cases

**Input 1:**  
`1 2 3 3 4 4 5`

**Output 1:**  
`1 2 5`

**Input 2:**  
`1 1 1 2 3`

**Output 2:**  
`2 3`

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

// LinkedList class with methods to insert, remove duplicates, and print the list
class LinkedList<T> {
    private Node<T> head;
    
    public LinkedList(){
        head = null;
    }
    
    // Inserts a new node with the given data at the end of the list
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
    
    // Removes all nodes that have duplicate numbers, leaving only distinct numbers
    private void removeDuplicates(){
        Node<T> dummy = new Node<T>(null); // Dummy node to handle edge cases
        dummy.next = head;
        Node<T> prev = dummy;
        while(prev.next != null){
            Node<T> cur = prev.next;
            boolean flag = false;
            // Move cur forward while there are duplicates
            while(cur.next != null && cur.data.equals(cur.next.data)){
                flag = true;
                cur = cur.next;
            }
            
            if(flag){
                // Skip all duplicates
                prev.next = cur.next;
            } else {
                // Move prev forward if no duplicate
                prev = prev.next;
            }
        }
        head = dummy.next;
    }
    
    // Prints the linked list elements in a single line
    private void print(){
        Node<T> cur = head;
        while(cur != null){
            System.out.print(cur.data + " ");
            cur = cur.next;
        }
    }
    
    // Main method to read input, process, and print output
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
