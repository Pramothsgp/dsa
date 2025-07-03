# Level Order Traversal of a Binary Tree

Help Kayal build a binary tree and print its level order traversal after inserting a new node.

---

## 📝 Problem Statement

Kayal is working on a task related to binary trees and needs your help.  
You must:

1. Build a binary tree from a list of node values.
2. Insert a new node with a given value at the end of the tree (level order).
3. Print the level order traversal of the binary tree.

---

## 📥 Input Format

- **First line:** Integer `n` — number of nodes in the initial binary tree.
- **Second line:** `n` space-separated integers — values of the existing nodes.
- **Third line:** Integer `m` — value of the node to insert at the end.

---

## 📤 Output Format

- If the binary tree is **not empty**, print the level order traversal after insertion (space-separated).
- If the binary tree is **empty**, print:

    ```
    Tree is empty
    ```

---

## 🔒 Constraints

- `1 ≤ n ≤ 15`
- `1 ≤ m ≤ 100`
- `0 ≤ elements ≤ 100`

---

## 💡 Sample Test Cases

### Input 1
```
5
1 2 3 4 5
6
```
**Output 1**
```
1 2 3 4 5 6 
```

---

### Input 2
```
7
1 2 3 4 5 6 7
10
```
**Output 2**
```
1 2 3 4 5 6 7 10 
```

---

### Input 3
```
6
12 78 65 43 65 15
89
```
**Output 3**
```
12 78 65 43 65 15 89 
```

---

### Input 4
```
0
```
**Output 4**
```
Tree is empty
```

---

## 🧑‍💻 Solution (Java)

```java
import java.util.*;

// Node class representing each node in the binary tree
class Node {
        int data;
        Node left, right;
        public Node(int data) {
                this.data = data;
                left = right = null;
        }
}

// BinaryTree class to build and manipulate the binary tree
class BinaryTree {
        Node root;

        // Constructor to build the tree from a list of values
        public BinaryTree(List<Integer> list) {
                root = null;
                buildTree(list);
        }

        // Builds the binary tree in level order from the list
        private void buildTree(List<Integer> list) {
                if (list.isEmpty()) return;
                root = new Node(list.remove(0));
                Queue<Node> q = new LinkedList<>();
                q.offer(root);
                while (!list.isEmpty()) {
                        Node cur = q.poll();
                        cur.left = new Node(list.remove(0));
                        q.offer(cur.left);

                        if (!list.isEmpty()) {
                                cur.right = new Node(list.remove(0));
                                q.offer(cur.right);
                        }
                }
        }

        // Inserts a new node at the end of the tree in level order
        public void insert(int data) {
                Queue<Node> q = new LinkedList<>();
                q.offer(root);
                while (!q.isEmpty()) {
                        Node cur = q.poll();
                        if (cur.left != null) {
                                q.offer(cur.left);
                        } else {
                                cur.left = new Node(data);
                                break;
                        }

                        if (cur.right != null) {
                                q.offer(cur.right);
                        } else {
                                cur.right = new Node(data);
                                break;
                        }
                }
                q.clear();
        }

        // Returns the level order traversal as a list
        public List<Integer> lot() {
                Queue<Node> q = new LinkedList<>();
                List<Integer> res = new ArrayList<>();
                q.offer(root);
                while (!q.isEmpty()) {
                        Node cur = q.poll();
                        res.add(cur.data);
                        if (cur.left != null) {
                                q.offer(cur.left);
                        }
                        if (cur.right != null) {
                                q.offer(cur.right);
                        }
                }
                return res;
        }

        // Main method to handle input and output
        public static void main(String[] args) {
                Scanner sc = new Scanner(System.in);
                int n = sc.nextInt();
                if (n == 0) {
                        System.out.println("Tree is empty");
                        return;
                }
                List<Integer> list = new ArrayList<>();
                for (int i = 0; i < n; i++) {
                        list.add(sc.nextInt());
                }
                BinaryTree tree = new BinaryTree(list);
                tree.insert(sc.nextInt());
                List<Integer> res = tree.lot();
                System.out.println(res.toString().replaceAll("\\[|\\]|,", ""));
        }
}
```