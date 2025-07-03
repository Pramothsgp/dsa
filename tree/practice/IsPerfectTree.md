# 🌳 Is the Binary Tree Perfect?

Alex, a software developer, is working on a project involving binary trees. He needs a program to determine if a given binary tree is **perfect**.

---

> ### 📝 **Definition**
> A **perfect binary tree** is a binary tree where:
> - **All internal nodes have exactly two children**
> - **All leaves are at the same level**

---

## 🌟 Example of a Perfect Binary Tree

```
        1
      /   \
     2     3
    / \   / \
   4  5  6   7
```

---

## 📥 Input Format

- **First line:** Integer `N` — total number of nodes in the tree.
- **Second line:** `N` space-separated integers — node values in level order.

## 📤 Output Format

- Print `"Yes"` if the binary tree is perfect.
- Otherwise, print `"No"`.

---

## 🔒 Constraints

- `1 ≤ N ≤ 20`
- `1 ≤ node values ≤ 100`

---

## 🧪 Sample Test Cases

### **Input 1**
```
7
1 2 3 4 5 6 7
```
**Output 1**
```
Yes
```

---

### **Input 2**
```
6
1 2 3 4 5 6
```
**Output 2**
```
No
```

---

## 💻 Java Solution

```java
import java.util.*;

// Node class representing each node in the binary tree
class Node<T> {
    T data;
    Node<T> left, right;

    public Node(T data) {
    this.data = data;
    left = right = null;
    }
}

// BinaryTree class to build and check if the tree is perfect
class BinaryTree<T> {
    Node<T> root;

    public BinaryTree(List<T> list) {
    root = null;
    buildTree(list);
    }

    // Build the binary tree in level order
    private void buildTree(List<T> list) {
    root = new Node<>(list.remove(0));
    Queue<Node<T>> q = new LinkedList<>();
    q.offer(root);
    while (!list.isEmpty()) {
        Node<T> cur = q.poll();
        cur.left = new Node<>(list.remove(0));
        q.offer(cur.left);
        if (!list.isEmpty()) {
        cur.right = new Node<>(list.remove(0));
        q.offer(cur.right);
        }
    }
    }

    // Check if the tree is perfect
    public boolean isPerfect() {
    int depth = this.depth(root);
    return isPerfect(root, depth, 0);
    }

    // Calculate the depth of the tree
    private int depth(Node<T> root) {
    return root == null ? 0 : Math.max(depth(root.left), depth(root.right)) + 1;
    }

    // Recursive check for perfection
    private boolean isPerfect(Node<T> root, int depth, int level) {
    if (root.left == null && root.right == null) {
        return depth == level + 1;
    }
    if (root.left == null || root.right == null) {
        return false;
    }
    return isPerfect(root.left, depth, level + 1) && isPerfect(root.right, depth, level + 1);
    }

    // Main method to read input and print result
    public static void main(String[] args) {
    Scanner sc = new Scanner(System.in);
    int n = sc.nextInt();
    List<Integer> list = new ArrayList<>();
    for (int i = 0; i < n; i++) {
        list.add(sc.nextInt());
    }
    BinaryTree<Integer> tree = new BinaryTree<>(list);
    System.out.println(tree.isPerfect() ? "Yes" : "No");
    }
}
```
