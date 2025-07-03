## 🚜 Problem Statement

Imagine you're developing a **smart irrigation system** for a large agricultural field. The field is divided into multiple zones, each monitored by a sensor that records **soil moisture levels**. These sensor readings are organized in a **binary tree** (level order), where each node represents a zone's soil moisture.

Your task: **Identify and report all zones with soil moisture levels below a given threshold**—helping determine which zones need irrigation.

---

### 📥 Input Format

- **First line:** Integer `n` — number of zones (nodes in the binary tree).
- **Second line:** `n` space-separated integers — soil moisture levels in level order.
- **Third line:** Integer `threshold` — the threshold soil moisture level.

---

### 📤 Output Format

- Print the soil moisture levels (space-separated) of all zones **below the threshold**, in **pre-order traversal**.
- If no zones meet the criteria, print `-1`.

---

### 📝 Constraints

- All input integers are **unique**.
- `1 ≤ n ≤ 15`
- `1 ≤ node values ≤ 150`
- `1 ≤ threshold ≤ 100`

---

### 💡 Sample Test Cases

#### Input 1
```
4
11 65 34 27
34
```
**Output 1**
```
11 27 
```

#### Input 2
```
6
6 7 4 2 3 5
2
```
**Output 2**
```
-1
```

---

### 🧑‍💻 Java Implementation

```java
import java.util.*;

// Node class representing each zone in the field
class Node<T> {
    T data;
    Node<T> left, right;
    public Node(T data) {
        this.data = data;
        left = right = null;
    }
}

// Binary Tree class for building and traversing the tree
class BST<T extends Comparable<T>> {
    Node<T> root;
    public BST() { root = null; }

    // Build the binary tree from level order data
    public void buildTree(List<T> data) {
        root = new Node<>(data.remove(0));
        Queue<Node<T>> q = new LinkedList<>();
        q.offer(root);
        while (!data.isEmpty()) {
            Node<T> cur = q.poll();
            cur.left = new Node<>(data.remove(0));
            q.offer(cur.left);
            if (!data.isEmpty()) {
                cur.right = new Node<>(data.remove(0));
                q.offer(cur.right);
            }
        }
    }

    // Find all fields (nodes) below the threshold in pre-order
    public List<T> findFieldsBelowThreshold(T key) {
        List<T> res = new ArrayList<>();
        findFields(root, key, res);
        return res;
    }

    // Pre-order traversal to collect nodes below threshold
    private void findFields(Node<T> root, T key, List<T> res) {
        if (root == null) return;
        if (root.data.compareTo(key) < 0) res.add(root.data);
        findFields(root.left, key, res);
        findFields(root.right, key, res);
    }

    // Main method to read input and produce output
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        BST<Integer> bst = new BST<>();
        List<Integer> nums = new ArrayList<>();
        for (int i = 0; i < n; i++) nums.add(sc.nextInt());
        bst.buildTree(nums);
        List<Integer> res = bst.findFieldsBelowThreshold(sc.nextInt());
        if (res.isEmpty()) {
            System.out.println(-1);
        } else {
            for (int num : res) System.out.printf("%d ", num);
        }
    }
}
```
