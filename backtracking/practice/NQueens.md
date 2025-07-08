# ♛ N-Queens Puzzle: Count Distinct Solutions

---

## 🧠 **Problem Description**

The **N-Queens puzzle** is the classic problem of placing `n` queens on an `n x n` chessboard such that:

* No two queens attack each other.

A queen can attack:

* ➡️ Horizontally
* ⬇️ Vertically
* ↘️ Diagonally (both directions)

Your task is to return the **number of distinct valid arrangements** of `n` queens on the board.

---

## 📥 Input Format

```
An integer n — size of the chessboard
```

---

## 📤 Output Format

```
A single integer — number of distinct solutions
```

---

## 🔒 Constraints

```
2 ≤ n ≤ 10
```

---

## 🧪 Sample Test Cases

### Input 1

```
4
```

### Output 1

```
2
```

### Input 2

```
3
```

### Output 2

```
0
```

### Input 3

```
9
```

### Output 3

```
352
```

---

## 📊 Explanation

* For `n = 4`, there are 2 valid configurations:

  * Both avoid queen-to-queen attacks across all rows, columns, and diagonals.

* For `n = 3`, **no** valid configuration exists where all 3 queens are safe.

---

## ✅ Java Solution (Clean & Optimized)

```java
import java.util.*;

public class NQueens {
    static int result = 0;

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();  // Read board size

        // Initialize three boolean arrays:
        // d1 → major diagonals (\)
        // d2 → minor diagonals (/)
        // col → column occupancy
        boolean[] d1 = new boolean[2 * n];
        boolean[] d2 = new boolean[2 * n];
        boolean[] col = new boolean[n];

        // Start recursive backtracking
        solve(n, 0, d1, d2, col);

        // Output the number of solutions
        System.out.println(result);
    }

    /**
     * Recursive function to place queens row-by-row
     * @param n Board size
     * @param row Current row being filled
     * @param d1 Major diagonals (\)
     * @param d2 Minor diagonals (/)
     * @param col Column flags
     */
    private static void solve(int n, int row, boolean[] d1, boolean[] d2, boolean[] col) {
        // Base case: all rows filled → one valid arrangement
        if (row == n) {
            result++;
            return;
        }

        // Try placing a queen in every column
        for (int i = 0; i < n; i++) {
            // Check if column and diagonals are free
            if (col[i] || d1[i + row] || d2[i - row + n]) continue;

            // Mark the current column and diagonals
            col[i] = d1[i + row] = d2[i - row + n] = true;

            // Move to the next row
            solve(n, row + 1, d1, d2, col);

            // Backtrack: unmark
            col[i] = d1[i + row] = d2[i - row + n] = false;
        }
    }
}
```

---

## 📌 Key Features

* ✔️ Uses **backtracking** with **pruning** to explore only valid configurations.
* 🧠 Tracks:

  * Columns (`col`)
  * Major diagonals (`d1`)
  * Minor diagonals (`d2`)
* ⚡ Efficient for values of `n` up to 10.

---
