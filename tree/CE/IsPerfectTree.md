## 🌳 Perfect Binary Tree Checker

Alex, a software developer, is working on a project involving binary trees. He needs to write a program to **determine if a given binary tree is perfect**.

> **Definition:**  
> A **perfect binary tree** is a binary tree in which **all internal nodes have exactly two children** and **all leaves are at the same level**.

---

### 📥 Input Format

- **First line:** Integer `N` — total number of nodes in the tree.
- **Second line:** `N` space-separated integers — the node values.

### 📤 Output Format

- Print `"Yes"` if the constructed binary tree is perfect.
- Print `"No"` otherwise.

*Follow the sample output format exactly.*

---

### 🔒 Constraints

- `1 ≤ N ≤ 20`
- `1 ≤ node values ≤ 100`

---

### 📝 Sample Test Cases

#### Input 1
```
7
1 2 3 4 5 6 7
```
**Output 1**
```
Yes
```

#### Input 2
```
6
1 2 3 4 5 6
```
**Output 2**
```
No
```

---

## 💻 Java Implementation

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

    public BinaryTree() {
        root = null;
    }

    // Builds the binary tree from a list of node values
    public void buildTree(List<T> datas) {
        root = new Node<>(datas.remove(0));
        Queue<Node<T>> q = new LinkedList<>();
        q.offer(root);
        while (!datas.isEmpty()) {
            Node<T> cur = q.poll();
            if (!datas.isEmpty()) {
                cur.left = new Node<>(datas.remove(0));
                q.offer(cur.left);
            }
            if (!datas.isEmpty()) {
                cur.right = new Node<>(datas.remove(0));
                q.offer(cur.right);
            }
        }
    }

    // Checks if the binary tree is perfect
    public boolean isPerfect() {
        int depth = findDepth(root);
        return isPerfect(root, depth, 0);
    }

    // Helper method to check if the tree is perfect recursively
    private boolean isPerfect(Node<T> root, int depth, int level) {
        // If leaf node, check if it's at the correct depth
        if (root.left == null && root.right == null) {
            return depth == level + 1;
        }
        // If an internal node is missing a child, not perfect
        if (root.left == null || root.right == null) {
            return false;
        }
        // Recursively check left and right subtrees
        return isPerfect(root.left, depth, level + 1) && isPerfect(root.right, depth, level + 1);
    }

    // Finds the depth of the tree
    private int findDepth(Node<T> root) {
        return root == null ? 0 : Math.max(findDepth(root.left), findDepth(root.right)) + 1;
    }

    // Main method to read input and output result
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        List<Integer> nums = new ArrayList<>();
        for (int i = 0; i < n; i++) {
            nums.add(sc.nextInt());
        }
        BinaryTree<Integer> bt = new BinaryTree<>();
        bt.buildTree(nums);
        System.out.println(bt.isPerfect() ? "Yes" : "No");
    }
}
```
