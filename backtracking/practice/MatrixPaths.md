# 🌟 Problem: All Possible Paths in a Matrix (Top-Left to Bottom-Right)

---

## 🧠 **Problem Description**

Given a 2D matrix of size `m x n`, you are required to find and print **all unique paths** from the **top-left corner** `(0, 0)` to the **bottom-right corner** `(m-1, n-1)`.

📌 The movement is **only allowed**:

* 👇 Downward
* 👉 Rightward

⚠️ At each step, **always explore the downward direction before the right**.

Each path must be printed as a **sequence of matrix values** from the starting cell to the destination cell.

---

## 📥 Input Format

```
m n                → 2 integers representing number of rows and columns
matrix elements    → m rows with n space-separated integers each
```

---

## 📤 Output Format

* Print each path on a new line
* Each path is space-separated
* Paths are printed in the order of first going **down**, then **right**

---

## 🔒 Constraints

```
1 ≤ m, n ≤ 5
Matrix values: Any integers
```

---

## 🔢 Sample Test Case 1

### Input

```
2 2
1 2
3 4
```

### Output

```
1 3 4
1 2 4
```

---

## 🔢 Sample Test Case 2

### Input

```
2 3
1 2 3
4 5 6
```

### Output

```
1 4 5 6
1 2 5 6
1 2 3 6
```

---

## 🔍 Explanation

From the top-left cell `(0, 0)`, we recursively explore:

1. **Downward first** (if possible)
2. Then **rightward** (if downward is not possible)

Each complete path that reaches the bottom-right is printed.

---

## ✅ Java Solution (Clean & Commented)

```java
import java.util.*;

public class Path {
    static int m, n;
    static int[][] grid;
    static List<String> result;

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // Step 1: Read matrix dimensions
        m = sc.nextInt();
        n = sc.nextInt();

        // Step 2: Read the matrix
        grid = new int[m][n];
        for (int i = 0; i < m; i++)
            for (int j = 0; j < n; j++)
                grid[i][j] = sc.nextInt();

        result = new ArrayList<>();

        // Step 3: Begin recursive DFS traversal from (0, 0)
        findPaths(0, 0, new ArrayList<>());

        // Step 4: Print all collected paths
        for (String path : result)
            System.out.println(path);
    }

    /**
     * Recursively finds all paths from (x, y) to bottom-right
     * @param x Current row index
     * @param y Current column index
     * @param path Current path being explored
     */
    private static void findPaths(int x, int y, List<Integer> path) {
        // Boundary check
        if (x >= m || y >= n)
            return;

        // Add current cell to the path
        path.add(grid[x][y]);

        // If reached destination, format and save the path
        if (x == m - 1 && y == n - 1) {
            result.add(formatPath(path));
            path.remove(path.size() - 1); // Backtrack
            return;
        }

        // Explore downward first
        findPaths(x + 1, y, path);

        // Then explore rightward
        findPaths(x, y + 1, path);

        // Backtrack (remove last cell before returning)
        path.remove(path.size() - 1);
    }

    /**
     * Utility to convert a list of integers to space-separated string
     */
    private static String formatPath(List<Integer> path) {
        StringBuilder sb = new StringBuilder();
        for (int num : path)
            sb.append(num).append(" ");
        return sb.toString().trim();
    }
}
```

---

## 🎯 Key Highlights

* ✔️ **DFS with backtracking** ensures all paths are explored correctly
* 📚 Uses `List<Integer>` to track each ongoing path
* 🧼 Clean formatting with `.trim()` ensures proper output
* 🎯 Focuses on **down → right** exploration order as required

---
