# 🌊 Maximize Land Mass by Flipping Water Cell

## 🌍 Problem Statement

You're working with a team of environmental researchers studying a terrain represented by a 2D grid:

* `0` → **land**
* `1` → **water**

A **land mass** is a group of connected land cells (`0`) that are **horizontally or vertically** adjacent (not diagonally).

Your task is to determine the **maximum possible land mass size** that can be achieved by **flipping exactly one water cell (`1`) to land (`0`)**.

---

## 🔢 Input Format

* Line 1: Two space-separated integers `m` and `n` — the number of rows and columns.
* Next `m` lines: Each line contains `n` space-separated integers (`0` or `1`) representing the terrain matrix.

### ✅ Constraints

* `1 ≤ m, n ≤ 100`
* At least one cell is water (`1`)

---

## 📤 Output Format

* A single integer: the **largest possible land mass size** after flipping one `1` to `0`.

---

## 🧪 Sample Test Case 1

### Input:

```
3 3
1 1 1
1 0 1
1 1 1
```

### Visualization:

```
1 1 1
1 0 1
1 1 1
```

### Explanation:

* There’s only **one land cell** in the middle.
* Flipping **any adjacent water cell** will connect to this land → land mass of size `2`.

### Output:

```
2
```

---

## 🧪 Sample Test Case 2

### Input:

```
2 4
1 1 0 1
1 1 1 1
```

### Visualization:

```
1 1 0 1
1 1 1 1
```

### Explanation:

* The single `0` is in `(0,2)` with no connected land.
* Best flip is to change `(0,1)` or `(0,3)` to `0` → connects with `(0,2)` → size `2`.

### Output:

```
2
```

---

## 💡 Java Code

```java
import java.util.*;

class Island {
    // Directions: right, down, left, up (for 4-connected neighbors)
    static final int[][] dir = {{0 , 1},{1 , 0},{0, -1} , {-1 , 0}};
    static int m , n;
    static int[][] grid; // Input matrix
    static int[][] ids;  // Stores unique island ID for each land cell
    
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);

        // Read dimensions
        m = sc.nextInt();
        n = sc.nextInt();

        grid = new int[m][n];
        ids = new int[m][n];

        // Map to store island ID and corresponding size
        Map<Integer,Integer> freq = new HashMap<>();

        // Read input matrix
        for(int i = 0; i < m; i++){
            for(int j = 0; j < n; j++){
                grid[i][j] = sc.nextInt();
            }
        }

        int id = -1; // Use negative values as island IDs

        // Assign IDs to all land masses using DFS
        for(int i = 0; i < m; i++){
            for(int j = 0; j < n; j++){
                if(grid[i][j] == 0 && ids[i][j] == 0){
                    int size = dfs(i , j , id); // Find size of land mass
                    freq.put(id , size);        // Store size against the island ID
                }
                id--; // Move to next unique ID
            }
        }

        int res = 0; // Result to store the max land mass possible after 1 flip

        // Check every water cell to see the best flip
        for(int i = 0; i < m; i++){
            for(int j = 0; j < n; j++){
                if(grid[i][j] == 1){
                    Set<Integer> set = new HashSet<>(); // To avoid counting the same island twice
                    int size = 1; // Flipping this water cell itself contributes 1
                    for(int[] d : dir){
                        int x = i + d[0];
                        int y = j + d[1];
                        // If neighbor is land and has an ID
                        if(isValid(x , y) && ids[x][y] != 0 && set.add(ids[x][y])){
                            size += freq.get(ids[x][y]); // Add unique neighbor island size
                        }
                    }
                    res = Math.max(res , size); // Update max size
                }
            }
        }

        // Final answer
        System.out.println(res);
    }

    // DFS to label connected land mass and count size
    private static int dfs(int i , int j , int id){
        if(!isValid(i , j) || grid[i][j] != 0 || ids[i][j] != 0) return 0;
        ids[i][j] = id; // Mark current cell with island ID
        int size = 1;
        for(int[] d : dir){
            size += dfs(i + d[0] , j + d[1] , id);
        }
        return size;
    }

    // Check if cell is within matrix bounds
    private static boolean isValid(int x , int y){
        return x >= 0 && y >= 0 && x < m  && y < n;
    }
}
```

---
