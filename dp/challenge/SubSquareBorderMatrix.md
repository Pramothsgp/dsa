# 🧠 CodeCell Innovation Challenge – Memory Grid Clean Borders

### 💻 Context:

You're given an `n x n` binary matrix simulating embedded system memory:

* `1` = Corrupted bit
* `0` = Clean (uncorrupted) bit

### ✅ Objective:

Check **if there exists at least one square subregion** (of size **2×2 or larger**) where **all 4 borders** consist **only of 0s**.

> ℹ️ The **inner part** of the square **can contain any values (0 or 1)**.

---

## 📥 Input Format:

```
n           → Size of matrix (2 ≤ n ≤ 7)  
n lines     → Each with n space-separated integers (0 or 1)
```

## 📤 Output Format:

```
true        → If a clean-bordered square exists  
false       → Otherwise
```

---

### 🧪 Sample Input 1:

```
6
1 1 1 1 1 1
1 0 0 0 0 1
1 0 0 0 0 1
1 0 0 0 0 1
1 0 0 0 0 1
1 1 1 1 1 1
```

### ✅ Sample Output 1:

```
true
```

---

### 🧪 Sample Input 2:

```
3
1 1 1
1 0 1
1 1 1
```

### ❌ Sample Output 2:

```
false
```

---

## 🧠 Java Solution — Clean, Stylish, and Fully Explained ✨

```java
import java.util.*;

class SubSquareMatrix {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // 📌 Step 1: Read matrix size
        int n = sc.nextInt();

        // 📌 Step 2: Read the n x n binary matrix
        int[][] grid = new int[n][n];
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                grid[i][j] = sc.nextInt();
            }
        }

        boolean found = false; // Flag to track if a valid square is found

        // 🔍 Step 3: Try every possible top-left corner (i, j)
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {

                // 📐 Step 4: Try all possible square sizes starting from 2x2
                for (int s = 2; i + s <= n && j + s <= n; s++) {
                    boolean valid = true;

                    // 🔎 Check top and bottom rows for 0s
                    for (int k = 0; k < s; k++) {
                        if (grid[i][j + k] != 0 || grid[i + s - 1][j + k] != 0) {
                            valid = false;
                            break;
                        }
                    }

                    // 🔎 Check left and right columns for 0s
                    for (int k = 0; k < s; k++) {
                        if (grid[i + k][j] != 0 || grid[i + k][j + s - 1] != 0) {
                            valid = false;
                            break;
                        }
                    }

                    // ✅ If all borders are 0, mark found and stop further checking
                    if (valid) {
                        found = true;
                        break;
                    }
                }

                // ⏹️ Early exit if found
                if (found) break;
            }
            if (found) break;
        }

        // 🖨️ Final Output
        System.out.println(found);
    }
}
```

---

## 📌 Summary

| Aspect           | Value                                   |
| ---------------- | --------------------------------------- |
| Matrix Type      | Square binary (n × n)                   |
| Goal             | Detect square with 0-bordered edges     |
| Inner Values     | Can be any (0 or 1)                     |
| Square Min Size  | 2 × 2                                   |
| Time Complexity  | O(n⁴) — acceptable due to small n (≤ 7) |
| Space Complexity | O(n²)                                   |

---
