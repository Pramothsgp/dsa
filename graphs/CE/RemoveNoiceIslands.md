# 🧼 Problem: Remove Enclosed Noise Islands in Binary Image

Ayesha is developing an image processing tool that detects **noise** in **binary images**. These images are represented as **2D grids** containing:

* `0` → white pixel
* `1` → black pixel

### 🟫 Definition of "Noise Islands":

> Groups of `1`s connected **horizontally or vertically** (not diagonally) that are **fully enclosed** within the image — i.e., they **do not touch the image border**.

### 🧽 Objective:

* Remove all enclosed islands by turning their `1`s into `0`s.
* Keep the `1`s that are **connected to the border** untouched.

---

## 📥 Input Format

1. Two integers: `m` and `n` — number of rows and columns.
2. `m` lines follow, each with `n` space-separated integers (`0` or `1`) representing the binary image.

---

## 📤 Output Format

* The modified matrix after cleaning, printed row by row, space-separated.

---

## 🔒 Constraints

* 1 ≤ m, n ≤ 1000
* Each element is either `0` or `1`
* Matrix may be rectangular

---

## 📌 Sample Input 1:

```
3 3
1 1 1
1 0 1
1 1 1
```

### 🔍 Explanation:

The only `0` is enclosed by `1`s, but since the surrounding `1`s are all touching the border, they are not considered noise.

### ✅ Output:

```
1 1 1
1 0 1
1 1 1
```

---

## 📌 Sample Input 2:

```
5 5
1 0 0 0 0
0 1 1 0 0
0 0 1 0 1
0 1 0 1 0
1 0 0 0 0
```

### 🔍 Explanation:

All islands of `1`s that do **not** touch the border are considered noise and must be turned into `0`s.

### ✅ Output:

```
1 0 0 0 0
0 0 0 0 0
0 0 0 0 1
0 0 0 0 0
1 0 0 0 0
```

---

# 👨‍💻 Java Code (With Comments)

```java
import java.util.*;

class NoiceRemover {

    // Directions: right, down, left, up (4-connected neighbors)
    private final static int[][] dir = new int[][] {
        {0, 1}, {1, 0}, {0, -1}, {-1, 0}
    };

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        // Read matrix dimensions
        int m = sc.nextInt();
        int n = sc.nextInt();
        
        // Read binary image
        int[][] image = new int[m][n];
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                image[i][j] = sc.nextInt();
            }
        }

        // Step 1: Start DFS from all 1s on the border to mark them as safe
        for (int i = 0; i < m; i++) {
            dfs(image, i, 0);       // Left border
            dfs(image, i, n - 1);   // Right border
        }

        for (int j = 0; j < n; j++) {
            dfs(image, 0, j);       // Top border
            dfs(image, m - 1, j);   // Bottom border
        }

        // Step 2: Convert all enclosed 1s to 0s, and restore border-connected 1s
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                if (image[i][j] == -1) {
                    image[i][j] = 1;  // Restore safe 1s
                } else if (image[i][j] == 1) {
                    image[i][j] = 0;  // Remove enclosed 1s (noise)
                }
            }
        }

        // Step 3: Print the cleaned matrix
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                System.out.printf("%d ", image[i][j]);
            }
            System.out.println();
        }
    }

    // DFS to mark all 1s connected to border as -1 (safe)
    private static void dfs(int[][] image, int i, int j) {
        if (!isValid(image, i, j)) return;

        image[i][j] = -1;  // Mark current 1 as visited/safe

        for (int[] d : dir) {
            dfs(image, i + d[0], j + d[1]);  // Explore all 4 directions
        }
    }

    // Valid position for DFS: within bounds and value == 1
    private static boolean isValid(int[][] image, int i, int j) {
        return i >= 0 && j >= 0 && i < image.length && j < image[0].length && image[i][j] == 1;
    }
}
```

---

### 🧠 Key Takeaways

* Use DFS to **preserve border-connected 1s**
* Then flip all **unvisited 1s** (enclosed noise) to 0
* Efficient even for large matrices (up to 1000 x 1000)

---
