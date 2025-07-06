# 🧫 BioCell Labs – Healing Simulation

### 🧪 **Problem Statement**

At BioCell Labs, a petri dish simulation is represented as a **2D grid**, where each cell can be:

* ✅ Healthy → Positive Value (`> 0`)
* ❌ Infected → Negative Value (`< 0`)
* ⚪ Neutral → Zero (`0`)

### 🎯 **Goal**

Determine how many *passes* (like days) are needed to heal all infected cells.

### 🔁 **Rules**

* Each pass, an **infected cell becomes healthy** if **at least one adjacent cell** (up/down/left/right) is already healthy.
* Healing occurs **simultaneously** across the grid.
* Neutral cells (`0`) are inert — cannot change or help others.
* If **any infected cell can’t ever be healed**, return `-1`.

---

### 📥 Input Format

```
Line 1: Two integers n and m — rows and columns of the grid.
Next n lines: m integers representing the grid.
```

---

### 📤 Output Format

```
Print the minimum number of passes required to heal all infected cells.
Print -1 if it's impossible.
```

---

### ✅ Constraints

* `1 ≤ n, m ≤ 1000`
* `-10⁹ ≤ matrix[i][j] ≤ 10⁹`

---

### 🧪 Sample Test Case 1

```
Input:
2 2
1 -1
-1 1

Output:
1
```

### 🧪 Sample Test Case 2

```
Input:
3 3
0 -1 -3
-1 0 -1
1 -1 -1

Output:
5
```

---

## 💻 Java Code Implementation

```java
import java.util.*;

class BioCell {
    // Directions: right, down, left, up
    private static final int[][] dir = new int[][] {
        {0, 1}, {1, 0}, {0, -1}, {-1, 0}
    };

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int m = sc.nextInt(); // Number of rows
        int n = sc.nextInt(); // Number of columns

        int[][] grid = new int[m][n];

        // Reading the grid
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                grid[i][j] = sc.nextInt();
            }
        }

        // Simulate healing process
        System.out.println(findDays(grid));
    }

    // Simulates the passes and returns minimum days to heal all infected
    private static int findDays(int[][] grid) {
        int infected = 0;  // Count of infected cells
        Queue<int[]> q = new LinkedList<>();

        // Initialize queue with all initially healthy cells
        for (int i = 0; i < grid.length; i++) {
            for (int j = 0; j < grid[0].length; j++) {
                if (grid[i][j] > 0) {
                    q.offer(new int[] {i, j, -1}); // {row, col, time}
                } else if (grid[i][j] < 0) {
                    infected++; // Count infected cells
                }
            }
        }

        int time = 0;

        // BFS to simulate spreading of health
        while (!q.isEmpty()) {
            int[] cur = q.poll();
            time = cur[2] + 1;

            for (int[] d : dir) {
                int x = cur[0] + d[0];
                int y = cur[1] + d[1];

                // If neighbor is infected and valid
                if (isValid(grid, x, y)) {
                    infected--;           // Heal one infected cell
                    grid[x][y] = 1;       // Mark it as healthy
                    q.offer(new int[] {x, y, time}); // Add to queue for next round
                }
            }
        }

        // If all infected cells are healed, return time; else -1
        return infected > 0 ? -1 : time;
    }

    // Checks if the coordinates are within bounds and cell is infected
    private static boolean isValid(int[][] grid, int x, int y) {
        return x >= 0 && y >= 0 && x < grid.length && y < grid[0].length && grid[x][y] < 0;
    }
}
```

---

### 🧠 Key Concepts Used:

* **Breadth-First Search (BFS)** for multi-source spreading (from healthy cells)
* **Level-wise traversal** to simulate time-based passes
* **Queue** to manage spreading across passes
* Handling of **neutral cells** and **isolated infections**
