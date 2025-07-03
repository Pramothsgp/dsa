# 🌳 Find Distance Between Nodes in a BST

Emma is working on a navigation system that needs to find the distance between two nodes in a **Binary Search Tree (BST)**. Implement a function to help Emma calculate the distance between two nodes.

---

## 📝 Problem Statement

Given a BST, find the number of edges in the shortest path between two given nodes.

---

## 📥 Input Format

- The first line contains an integer `n`, representing the number of nodes to be inserted into the BST.
- The second line consists of `n` space-separated integers, representing the values to be inserted.
- The third line consists of two integers `n1` and `n2`, representing the values of the two nodes.

---

## 📤 Output Format

- Print the distance (number of edges) between the two given nodes.

---

## 📚 Constraints

- `1 ≤ n ≤ 25`
- `1 ≤ tree elements, n1, n2 ≤ 100`

---

## 💡 Example

### Input
```
7
20 10 30 5 15 25 35
5 35
```

### Output
```
4
```

**Explanation:**  
The BST for the nodes is:

```
    20
   /  \
 10    30
 / \   / \
5  15 25 35
```

The path from 5 to 35 is:  
5 → 10 → 20 → 30 → 35 (4 steps).

---

## 🧪 Sample Test Cases

### Input 1
```
7
20 10 30 5 15 25 35
5 35
```
**Output 1**
```
4
```

### Input 2
```
5
56 64 8 9 43
8 43
```
**Output 2**
```
2
```

---

## 💻 Java Solution

```java
import java.util.*;

// Node class representing each node in the BST
class Node<T> {
    T data;
    Node<T> left, right;
    public Node(T data){
        this.data = data;
        left = right = null;
    }
}

// BST class with generic type
class BST<T extends Comparable<T>> {
    private Node<T> root;

    public BST() {
        root = null;
    }

    // Insert a new node into the BST
    public void insert(T data) {
        root = insert(root, data);
    }

    // Helper method for insertion
    private Node<T> insert(Node<T> root, T data) {
        if (root == null) {
            return new Node<T>(data);
        }
        if (data.compareTo(root.data) < 0) {
            root.left = insert(root.left, data);
        } else if (data.compareTo(root.data) > 0) {
            root.right = insert(root.right, data);
        }
        return root;
    }

    // Find distance between two nodes
    public int findDistance(T a, T b) {
        Node<T> lca = findLCA(root, a, b); // Find Lowest Common Ancestor
        int dist1 = findDistance(lca, a);  // Distance from LCA to first node
        int dist2 = findDistance(lca, b);  // Distance from LCA to second node
        return dist1 + dist2;
    }

    // Find Lowest Common Ancestor (LCA) of two nodes
    private Node<T> findLCA(Node<T> root, T a, T b) {
        if (root == null) return null;
        if (root.data.compareTo(a) > 0 && root.data.compareTo(b) > 0) {
            return findLCA(root.left, a, b);
        } else if (root.data.compareTo(a) < 0 && root.data.compareTo(b) < 0) {
            return findLCA(root.right, a, b);
        } else {
            return root;
        }
    }

    // Find distance from root to a given node
    private int findDistance(Node<T> root, T a) {
        int distance = 0;
        while (root != null) {
            if (root.data.equals(a)) {
                return distance;
            } else if (root.data.compareTo(a) > 0) {
                distance++;
                root = root.left;
            } else {
                distance++;
                root = root.right;
            }
        }
        return -1; // Node not found
    }

    // Main method to read input and print output
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        BST<Integer> bst = new BST<>();
        int n = sc.nextInt();
        for (int i = 0; i < n; i++) {
            bst.insert(sc.nextInt());
        }
        System.out.println(bst.findDistance(sc.nextInt(), sc.nextInt()));
    }
}
```
