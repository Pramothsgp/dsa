# 🏫 Debate Team Assignment — Check for Bipartite Graph

### 📌 **Problem Overview**

A university wants to split students into two debate teams:
**Team Alpha** and **Team Beta**.

Each student has a list of **rivalries** — students they **refuse to be on the same team with**.
You must determine whether this is possible by checking if the rivalry graph is **bipartite**.

A **self-loop** (a student refusing to participate unless with themselves) makes this **impossible**.

---

### 📥 **Input Format**

* `Line 1`: An integer `n` — number of students (nodes).
* Next `n` lines: Rivalry list (adjacency list) for each student, ending with `-1`.

---

### 📤 **Output Format**

* Print `true` if a valid 2-team split is possible.
* Print `false` otherwise.

---

### ✅ **Constraints**

* `1 ≤ n ≤ 10⁴`
* Undirected graph (if A is rival of B, B is rival of A)
* Graph is connected
* May contain **self-loops** (invalid case)

---

### 🧪 **Sample Input 1**

```
3
1 -1
0 2 -1
1 -1
```

**Output:**

```
true
```

---

### 🧪 **Sample Input 2**

```
3
1 2 -1
0 2 -1
0 1 -1
```

**Output:**

```
false
```

---

## 🧠 Java Implementation

```java
import java.util.*;

class IsBiParted {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        int n = sc.nextInt();     // Number of students
        sc.nextLine();            // Consume leftover newline after nextInt()

        List<List<Integer>> graph = new ArrayList<>();
        
        // Initialize adjacency list
        for(int i = 0; i < n; i++) {
            graph.add(new ArrayList<>());
        }

        try {
            // Read rivalry graph input
            for(int i = 0; i < n; i++) {
                String[] rivals = sc.nextLine().split(" ");
                for(String r : rivals) {
                    int num = Integer.parseInt(r);
                    if(num == -1) break;     // End of this line's rival list
                    graph.get(i).add(num);   // Add rival edge
                }
            }

            // Run bipartite check
            System.out.println(isBiPartite(graph));
        } catch (Exception e) {
            // Catch malformed input or invalid node references
            System.out.println(false);
        }
    }

    private static boolean isBipartite(List<List<Integer>> graph) {
        int n = graph.size();
        int[] team = new int[n];         // Team assignments: 0 or 1
        Arrays.fill(team, -1);           // -1 indicates unassigned

        Queue<Integer> q = new LinkedList<>();
        q.offer(0);                      // Start BFS from node 0
        team[0] = 0;                     // Assign to Team Alpha (0)

        while(!q.isEmpty()) {
            int cur = q.poll();
            for(int neighbour : graph.get(cur)) {
                if(team[neighbour] == -1) {
                    team[neighbour] = 1 - team[cur]; // Assign opposite team
                    q.offer(neighbour);
                } else if(team[neighbour] == team[cur]) {
                    return false;       // Rival on same team — not bipartite
                }
            }
        }

        return true; // Successfully assigned all with no conflict
    }
}
```

---

## 🧾 Notes:

* The code uses **Breadth-First Search (BFS)** for graph traversal and team assignment.
* It gracefully handles invalid inputs or self-loops using a `try-catch` block.
* BFS starts from student `0`, as the graph is assumed to be **connected**.
