# 🌳 Level Order Traversal in a Binary Search Tree

Tim is learning about **binary search trees (BST)** and their traversal techniques.  
He wants to implement a program that constructs a BST by inserting nodes and then performs a **level order traversal**.

---

## 📥 Input Format

- Space-separated integers, representing the nodes to be inserted into the BST.
- Input ends when a non-positive integer (≤ 0) is entered.

---

## 📤 Output Format

- Print the elements of the BST in **level-order traversal** (breadth-first order), separated by spaces.

---

## 📝 Constraints

- 1 ≤ node values ≤ 100

---

## 💡 Example

**Input:**
```
2 3 1 0
```

**Output:**
```
2 1 3 
```

**Explanation:**  
- `2` is the root (level 1).
- `1` is the left child, `3` is the right child (level 2).
- Level order traversal: `2 1 3`

---

## 🧪 Sample Test Cases

| Input                | Output        |
|----------------------|--------------|
| `2 3 1 0`            | `2 1 3 `     |
| `3 5 4 7 1 -6`       | `3 1 5 4 7 ` |

---

## 🚀 Java Implementation

```java
import java.util.*;

// Node class representing each node in the BST
class Node<T>{
    T data;
    Node<T> left, right;
    public Node(T data){
        this.data = data;
        left = right = null;
    }
}

// BST class with insert and level order traversal methods
class BST<T extends Comparable<T>>{
    private Node<T> root;

    public BST(){
        root = null;
    }

    // Insert a new node into the BST
    public void insert(T data){
        root = insert(root, data);
    }

    // Helper method for insertion (recursive)
    private Node<T> insert(Node<T> root, T data){
        if(root == null){
            return new Node<T>(data);
        }
        if(root.data.compareTo(data) > 0){
            root.left = insert(root.left, data);
        } else if(root.data.compareTo(data) < 0){
            root.right = insert(root.right, data);
        }
        return root;
    }

    // Level Order Traversal (Breadth-First Search)
    public List<T> lot(){
        Queue<Node<T>> q = new LinkedList<>();
        List<T> list = new ArrayList<>();
        if(root != null) q.offer(root);
        while(!q.isEmpty()){
            Node<T> cur = q.poll();
            list.add(cur.data);
            if(cur.left != null) q.offer(cur.left);
            if(cur.right != null) q.offer(cur.right);
        }
        return list;
    }
}

// Main class to read input and print level order traversal
class Solution{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int data;
        BST<Integer> bst = new BST<>();
        // Read input and insert nodes until a non-positive integer is entered
        while((data = sc.nextInt()) > 0){
            bst.insert(data);
        }
        // Get the level order traversal result
        List<Integer> res = bst.lot();
        // Print the result
        for(int num : res){
            System.out.printf("%d ", num);
        }
    }
}
```

---
