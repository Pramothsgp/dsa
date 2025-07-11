# 🧮 Problem Statement: Maximum Sum of Square Submatrix

Given a **2D matrix of integers** of size `m x n`, and a **positive integer `size`**, your goal is to:

👉 Find the **maximum sum of any square submatrix of dimension `size x size`**.

---

## 📥 Input Format

```
First line: Two space-separated integers m and n (rows and columns)
Next m lines: Each line has n space-separated integers (matrix elements)
Last line: A single integer 'size' (dimension of square submatrix)
```

## 📤 Output Format

```
Single integer — the maximum sum of any size×size square submatrix.
```

---

## 🧪 Sample Input 1

```
4 5
1 1 1 1 1
1 2 2 2 1
1 2 9 2 1
1 1 1 1 1
3
```

### Output:

```
22
```

## 🧪 Sample Input 2

```
3 3
1 2 3
4 5 6
7 8 9
2
```

### Output:

```
28
```

---

## ✅ Java Code (Efficient with Prefix Sum + Comments)

```java
import java.util.*;

class MaxSquareSum {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // Step 1: Read matrix dimensions
        int m = sc.nextInt();
        int n = sc.nextInt();

        // Step 2: Read the matrix
        int[][] grid = new int[m][n];
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                grid[i][j] = sc.nextInt();
            }
        }

        // Step 3: Read the size of the square submatrix
        int size = sc.nextInt();

        // Step 4: Create prefix sum matrix of size (m+1)x(n+1) for 1-based indexing
        int[][] prefix = new int[m + 1][n + 1];

        // Fill the prefix sum matrix
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                prefix[i][j] = grid[i - 1][j - 1] 
                             + prefix[i - 1][j] 
                             + prefix[i][j - 1] 
                             - prefix[i - 1][j - 1];
            }
        }

        // Step 5: Find the maximum sum of any size x size submatrix
        int maxSum = Integer.MIN_VALUE;

        for (int i = size; i <= m; i++) {
            for (int j = size; j <= n; j++) {
                // Get sum of submatrix from (i-size+1,j-size+1) to (i,j)
                int sum = prefix[i][j]
                        - prefix[i - size][j]
                        - prefix[i][j - size]
                        + prefix[i - size][j - size];

                maxSum = Math.max(maxSum, sum);
            }
        }

        // Step 6: Output the result
        System.out.println(maxSum);
    }
}
```

---

## 🧠 Explanation

We use a **prefix sum matrix** to calculate submatrix sums in constant time (`O(1)`).
This avoids recalculating sums for each submatrix, reducing time complexity from `O(m * n * size^2)` to `O(m * n)`.

### Prefix Sum Logic:

For any submatrix from `(r1,c1)` to `(r2,c2)`,
we can compute sum in constant time as:

```
sum = prefix[r2][c2] 
    - prefix[r1 - 1][c2] 
    - prefix[r2][c1 - 1] 
    + prefix[r1 - 1][c1 - 1]
```

---

## ⏱️ Time & Space Complexity

| Metric               | Value      |
| -------------------- | ---------- |
| **Time Complexity**  | `O(m * n)` |
| **Space Complexity** | `O(m * n)` |

---
