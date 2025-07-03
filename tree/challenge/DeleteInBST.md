# Delete a Node in a Binary Search Tree (BST)

John is learning about **Binary Search Trees (BST)** in his computer science class. He wants to create a program that allows users to **delete a node with a given value** from a BST and print the remaining nodes.

Your task is to implement a function to help him delete a node with a given value from a BST.

---

## 📝 Input Format

- **First line:** An integer `N` — the number of nodes in the BST.
- **Second line:** `N` space-separated integers — the values of the BST nodes.
- **Third line:** An integer `V` — the value to delete from the BST.

---

## 📤 Output Format

- Print the space-separated values in the BST using **in-order traversal** after deleting the specified value.
- If the value is not present, print the in-order traversal of the original BST.

---

## 📚 Constraints

- `1 ≤ N ≤ 10`
- `1 ≤ node values ≤ 100`
- `1 ≤ V ≤ 100`
- All node values are **unique**.

---

## 💡 Sample Test Cases

### Input 1
```
5
10 5 15 2 7
15
```
**Output 1**
```
2 5 7 10 
```

---

### Input 2
```
7
50 30 70 20 40 60 80
50
```
**Output 2**
```
20 30 40 60 70 80 
```

---

### Input 3
```
3
4 7 6
8
```
**Output 3**
```
4 6 7 
```

---

## 🚀 Java Implementation

```java
import java.util.*;

// Node class representing each node in the BST
class Node<T> {
    T data;
    Node<T> left, right;

    public Node(T data) {
        this.data = data;
        left = right = null;
    }
}

// BST class with generic type T (must be Comparable)
class BST<T extends Comparable<T>> {
    Node<T> root;

    public BST() {
        root = null;
    }

    public void insert(T data) {
        root = insert(root, data);
    }

    private Node<T> insert(Node<T> root, T data) {
        if (root == null) return new Node<>(data);
        if (data.compareTo(root.data) < 0)
            root.left = insert(root.left, data);
        else if (data.compareTo(root.data) > 0)
            root.right = insert(root.right, data);
        return root;
    }

    public void delete(T key) {
        root = delete(root, key);
    }

    private Node<T> delete(Node<T> root, T key) {
        if (root == null) return root;
        if (key.compareTo(root.data) < 0)
            root.left = delete(root.left, key);
        else if (key.compareTo(root.data) > 0)
            root.right = delete(root.right, key);
        else {
            if (root.left == null) return root.right;
            if (root.right == null) return root.left;
            Node<T> successor = getMin(root.right);
            root.data = successor.data;
            root.right = delete(root.right, successor.data);
        }
        return root;
    }

    private Node<T> getMin(Node<T> root) {
        while (root != null && root.left != null) root = root.left;
        return root;
    }

    public void print() {
        inOrder(root);
    }

    private void inOrder(Node<T> root) {
        if (root == null) return;
        inOrder(root.left);
        System.out.print(root.data + " ");
        inOrder(root.right);
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        BST<Integer> bst = new BST<>();
        for (int i = 0; i < n; i++) {
            bst.insert(sc.nextInt());
        }
        bst.delete(sc.nextInt());
        bst.print();
    }
}
```

---
