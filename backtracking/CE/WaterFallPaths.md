# 🧭 Print All Paths in Matrix (Right and Down Only)

### ✅ Problem Statement

Given an `m x n` matrix, print **all possible paths** from the **top-left cell** to the **bottom-right cell**, **moving only down or right** at each step.

---

### 📥 Input Format

* The first line contains two integers `m` and `n` – number of rows and columns.
* The next `m` lines contain `n` integers each – representing the matrix values.

---

### 📤 Output Format

* Print all the paths from top-left to bottom-right.
* Each path is printed as space-separated integers on a new line.

---

### 🔐 Constraints

* `1 ≤ m, n ≤ 5`
* Matrix values are integers

---

### 🧪 Sample Test Cases

#### Input 1:

```
2 3
1 2 3
4 5 6
```

#### Output 1:

```
1 4 5 6
1 2 5 6
1 2 3 6
```

#### Input 2:

```
2 2
1 2
3 4
```

#### Output 2:

```
1 3 4
1 2 4
```

---

### 💡 Explanation

From a given cell, you can only:

* Move **right** (`→`)
* Move **down** (`↓`)

Use **DFS (Depth First Search)** with **backtracking** to explore all valid paths to the destination.

---

### 🧠 Java Code with Backtracking

```java
import java.util.*;

class Paths {
    static List<String> res;

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int m = sc.nextInt();  // rows
        int n = sc.nextInt();  // columns
        
        int[][] grid = new int[m][n];
        
        // Reading matrix values
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                grid[i][j] = sc.nextInt();
            }
        }

        res = new ArrayList<>();
        dfs(grid, 0, 0, new ArrayList<>());
        
        // Print each result path
        for (String path : res) {
            System.out.println(path);
        }
    }

    // DFS function
    private static void dfs(int[][] grid, int x, int y, List<Integer> path) {
        int m = grid.length;
        int n = grid[0].length;

        // Out of bounds check
        if (x >= m || y >= n) return;

        path.add(grid[x][y]);

        // Reached destination
        if (x == m - 1 && y == n - 1) {
            res.add(listToString(path));
        } else {
            dfs(grid, x + 1, y, path); // move down
            dfs(grid, x, y + 1, path); // move right
        }

        path.remove(path.size() - 1); // backtrack
    }

    // Convert list to space-separated string
    private static String listToString(List<Integer> list) {
        StringBuilder sb = new StringBuilder();
        for (int num : list) {
            sb.append(num).append(" ");
        }
        return sb.toString().trim();
    }
}
```

---

### ⏱ Time Complexity

* Maximum paths = $\binom{m+n-2}{m-1}$
* For small grid sizes (max 5x5), this is manageable.

---
