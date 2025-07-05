# 🏢 Corporate Directory System – BFS Traversal

## 📝 Problem Statement

You’ve been hired to build a **corporate directory system** for a tech company. The company’s **organizational structure** is represented as a **tree**, where:

* Each employee has a **unique name**.
* Each employee may have **zero or more direct reports** (children).
* The hierarchy is a **connected, acyclic tree**, rooted at the **CEO**.

---

## 🎯 Objective

Implement a function called `breadthFirstSearch` which:

* Traverses the tree **level by level** from the CEO (top) using **Breadth-First Search (BFS)**.
* Stores and returns the names of employees in **BFS order**.
* Helps the HR system print the **top-down hierarchy** in a readable format.

---

## 📥 Input Format

1. **Line 1**: An integer `n` — total number of employees.
2. **Next `n` lines**: Each line describes an employee in the following format:

   ```
   EmployeeName NumberOfReports Report1 Report2 ...
   ```

> ✅ The first line is **always the CEO**.

---

## 📤 Output Format

* A **single line** of employee names in **BFS order**, separated by **spaces**.

---

## 📌 Constraints

* `1 ≤ n ≤ 1000`
* Names are unique, case-sensitive strings (e.g., `A`, `Node1`)
* The structure is a valid **acyclic tree**

---

## ✅ Sample Input 1

```
3
A 2 B C
B 0
C 0
```

### ✅ Sample Output 1

```
A B C
```

---

## ✅ Sample Input 2

```
7
A 2 B C
B 2 D E
C 2 F G
D 0
E 0
F 0
G 0
```

### ✅ Sample Output 2

```
A B C D E F G
```

---

## 👨‍💻 Java Code

```java
import java.util.*;

class Graph {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        Map<String, List<String>> graph = new HashMap<>();
        String src = "";

        // Read the organization chart
        for (int i = 0; i < n; i++) {
            String name = sc.next();
            if (i == 0) src = name; // First employee is always the CEO
            int count = sc.nextInt();
            List<String> reports = new ArrayList<>();
            for (int j = 0; j < count; j++) {
                reports.add(sc.next());
            }
            graph.put(name, reports);
        }

        // Perform BFS and print result
        List<String> result = bfs(graph, src);
        System.out.println(String.join(" ", result));
    }

    private static List<String> bfs(Map<String, List<String>> graph, String src) {
        List<String> res = new ArrayList<>();
        Queue<String> queue = new LinkedList<>();
        Set<String> visited = new HashSet<>();

        queue.offer(src);

        while (!queue.isEmpty()) {
            String current = queue.poll();
            if (visited.contains(current)) continue;

            res.add(current);
            visited.add(current);

            List<String> neighbors = graph.getOrDefault(current, new ArrayList<>());
            for (String neighbor : neighbors) {
                if (!visited.contains(neighbor)) {
                    queue.offer(neighbor);
                }
            }
        }

        return res;
    }
}
```

---

## 💡 Explanation

* The program reads employee data and builds an **adjacency list** to represent the org chart.
* It then performs **BFS traversal** starting from the CEO.
* All employee names are printed in **top-down, left-to-right** order.

---

## 🏁 Output Example

For the input:

```
3
A 2 B C
B 0
C 0
```

The output will be:

```
A B C
```

---

## 📚 Time and Space Complexity

| Metric           | Value  |
| ---------------- | ------ |
| Time Complexity  | `O(n)` |
| Space Complexity | `O(n)` |

> `n` is the number of employees. BFS ensures each node is visited exactly once.

---

