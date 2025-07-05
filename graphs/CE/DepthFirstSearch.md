
# 🗂️ Problem: DFS Traversal of Folder Structure

Aditi is building a **file explorer application**, where folders and subfolders are represented using a **tree data structure**. Each folder has a **name** and may contain other subfolders (children).

She wants to **display the folder hierarchy** using **Depth-First Search (DFS)** traversal, starting from the **root folder (index 0)** and visiting subfolders **from left to right**.

---

## ✅ Objective

Perform **DFS traversal** on a given folder structure and **print the names** of folders in the order they are visited.

---

## 📥 Input Format

1. `n` — an integer representing the total number of nodes (folders).
2. `n` space-separated strings — names of the nodes.
3. `m` — number of parent-child relationships.
4. Next `m` lines — each line contains two integers:

   * `parent_index`: index of the parent node
   * `child_index`: index of the child node

---

## 📤 Output Format

* Print:

```
DFS Traversal Order:
<space-separated folder names in DFS order>
```

---

## 🔒 Constraints

* 1 ≤ n ≤ 1000
* 0 ≤ m ≤ n − 1
* Each node name is a string of up to 10 alphabetic characters
* The input forms a valid **acyclic tree** rooted at index `0`

---

## 📌 Sample Input 1

```
5
A B C D E
4
0 1
0 2
1 3
1 4
```

### 🔍 Explanation:

```
        A
       / \
      B   C
     / \
    D   E
```

---

## ✅ Sample Output 1

```
DFS Traversal Order:
A B D E C
```

---

## 📌 Sample Input 2

```
4
A B C D
3
0 1
0 2
0 3
```

### 🔍 Explanation:

```
     A
   / | \
  B  C  D
```

---

## ✅ Sample Output 2

```
DFS Traversal Order:
A B C D
```

---

# 👨‍💻 Java Code (DFS Traversal with Comments)

```java
import java.util.*;

class FileSystem {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // Read the number of folders (nodes)
        int n = sc.nextInt();

        // Read folder names and store in array
        String[] nodes = new String[n];
        for (int i = 0; i < n; i++) {
            nodes[i] = sc.next(); // input each folder name
        }

        // Read number of relationships (edges)
        int e = sc.nextInt();

        // Create adjacency list to represent folder structure
        List<List<Integer>> graph = new ArrayList<>();
        for (int i = 0; i < n; i++) {
            graph.add(new ArrayList<>()); // initialize empty list for each folder
        }

        // Read the parent-child relationships
        for (int i = 0; i < e; i++) {
            int u = sc.nextInt(); // parent index
            int v = sc.nextInt(); // child index
            graph.get(u).add(v);  // add child to parent's list
        }

        // Track visited folders
        boolean[] visited = new boolean[n];

        // Store the DFS traversal order
        List<Integer> res = new ArrayList<>();

        // Perform DFS starting from root node (index 0)
        dfs(graph, visited, res, 0);

        // Output traversal order
        System.out.println("DFS Traversal Order:");
        for (int i : res) {
            System.out.printf("%s ", nodes[i]); // print folder names
        }
    }

    // DFS function to traverse the folder tree
    private static void dfs(List<List<Integer>> graph, boolean[] visited, List<Integer> res, int src) {
        res.add(src);           // add current folder to result
        visited[src] = true;    // mark folder as visited

        for (int v : graph.get(src)) {
            if (!visited[v]) {
                dfs(graph, visited, res, v); // recursively visit children
            }
        }
    }
}
```

---

### 🧠 Key Concepts Used:

* Tree representation using **adjacency list**
* **Depth-First Search (DFS)** traversal
* Tracking visited nodes to avoid revisiting
* Recursion for traversal

---
