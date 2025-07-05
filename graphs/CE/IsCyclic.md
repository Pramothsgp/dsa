
## 🚀 Problem: Detect Cycles in Directed Graph (NetMap Inc.)

### 🧠 Concept:

Given a directed graph (as an adjacency list), determine if there is any **cycle**, including:

* Self-loop (`i → i`)
* Indirect loops (`i → j → k → i`)

We use **DFS with recursion stack** to track back-edges that form a cycle.

---

### ✅ Java Code

```java
import java.util.*;

class NetMap {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int nodes = sc.nextInt();  // Number of tasks (nodes)
        sc.nextLine();

        List<List<Integer>> graph = new ArrayList<>();

        // Building the adjacency list
        for (int i = 0; i < nodes; i++) {
            List<Integer> pipes = new ArrayList<>();
            if (sc.hasNext()) {
                String[] line = sc.nextLine().split("\\s+");
                for (String s : line) {
                    if (!s.isEmpty())
                        pipes.add(Integer.parseInt(s)); // Add outbound edges
                }
            }
            graph.add(pipes); // Add the list to the graph
        }

        // Detect and print if a cycle exists
        System.out.println(detectCycle(graph));
    }

    /**
     * Detects cycle in the entire graph using DFS traversal
     */
    private static boolean detectCycle(List<List<Integer>> graph) {
        int n = graph.size();
        boolean[] visited = new boolean[n];   // Tracks visited nodes
        boolean[] recStack = new boolean[n];  // Tracks recursion stack (current path)

        // Check for cycles in each disconnected component
        for (int i = 0; i < n; i++) {
            if (!visited[i]) {
                if (dfs(graph, i, visited, recStack)) {
                    return true;  // Cycle found
                }
            }
        }
        return false; // No cycle found
    }

    /**
     * DFS helper to detect cycle using recursion stack
     */
    private static boolean dfs(List<List<Integer>> graph, int node, boolean[] visited, boolean[] recStack) {
        visited[node] = true;       // Mark node as visited
        recStack[node] = true;      // Mark node in current DFS path

        for (int neighbour : graph.get(node)) {
            if (!visited[neighbour]) {
                if (dfs(graph, neighbour, visited, recStack)) {
                    return true; // Found cycle in deeper recursion
                }
            } else if (recStack[neighbour]) {
                return true; // Back-edge found → cycle
            }
        }

        recStack[node] = false;     // Remove node from current path
        return false;               // No cycle in this path
    }
}
```

---

### 🧪 Sample Input 1:

```
3
1
2

```

#### ✅ Output:

```
false
```

---

### 🧪 Sample Input 2:

```
6
1
2
0 3
4
5
3
```

#### ✅ Output:

```
true
```

---

### 📈 Time Complexity:

* `O(V + E)` where `V` = number of nodes, `E` = number of edges

### 🧵 Space Complexity:

* `O(V)` for `visited` and `recStack` arrays
* Recursive stack space up to `O(V)` in worst case

---
