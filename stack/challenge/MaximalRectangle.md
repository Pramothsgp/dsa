# 🏞️ Maximal Rectangle

## 🚩 Problem Statement

A city plans to construct a new public park and needs your help to find the **largest possible area** where the park can be built without disturbing any existing infrastructure.

You are given a 2D grid (`land`), representing a top-down view of the city:

- `0` → Unused land (can be used for the park)
- `1` → Land already in use (must be avoided)

**Task:**  
Determine the **maximum area of a rectangle made only of 0s** (unused land).

> - The rectangle must be continuous and perfectly shaped (not L-shaped).
> - If no rectangle of unused land exists, return `0`.

---

### 📥 Input Format

- The first line: integers `m` and `n` (number of rows and columns).
- Next `m` lines: each contains `n` space-separated integers representing the land grid.

### 📤 Output Format

- Print a single integer: the area of the largest rectangle made up entirely of unused land (`0`s).

---

### ⛔ Constraints

- `1 ≤ m, n ≤ 200`
- Each cell `land[i][j]` is either `0` (unused) or `1` (used)

---

## 🧪 Sample Test Cases

#### **Input 1**
```
2 2
0 0
0 1
```
**Output 1**
```
2
```

---

#### **Input 2**
```
3 3
1 1 1
1 0 1
1 0 1
```
**Output 2**
```
2
```

---

## 💡 Solution 1: Brute Force Approach

A straightforward way is to check every possible rectangle of 0s.

```java
import java.util.*;

class MaxsizeRectange{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int m = sc.nextInt(); 
        int n = sc.nextInt(); 
        int[][] grid = new int[m][n];
        
        // Read the grid input
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                grid[i][j] = sc.nextInt();
            }
        }
        
        System.out.println(maxRectangle(grid));
    }
    
    // Brute force method to find the maximal rectangle of 0s
    private static int maxRectangle(int[][] grid){
        int m = grid.length , n = grid[0].length;
        int res = 0;
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                if(grid[i][j] == 0){
                    int minWidth = n;
                    // Try to extend the rectangle downwards
                    for(int row = i;row < m && grid[row][j] == 0;row++){
                        int width = 0;
                        int col = j;
                        // Find the width of 0s in the current row
                        while(col < n && grid[row][col] == 0){
                            width++;
                            col++;
                        }
                        minWidth = Math.min(minWidth , width);
                        int height = row - i + 1;
                        res = Math.max(res , minWidth * height);
                    }
                }
            }
        }
        return res;
    }
}
```

---

## ⚡ Solution 2: Optimized Histogram Approach

This approach treats each row as the base of a histogram and uses a stack to find the largest rectangle efficiently.

```java
import java.util.*;

class MaxsizeRectange{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int m = sc.nextInt(); 
        int n = sc.nextInt(); 
        int[][] grid = new int[m][n];
        
        // Read the grid input
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                grid[i][j] = sc.nextInt();
            }
        }
        
        System.out.println(maxRectangle(grid));
    }
    
    // Optimized method using histogram technique
    private static int maxRectangle(int[][] grid){
        int m = grid.length , n = grid[0].length;
        int res = 0;
        int[] height = new int[n];
        
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                // Build up the histogram of 0s for each column
                if(grid[i][j] == 0){
                    height[j]++;
                } else{
                    height[j] = 0;
                }
            }
            // Find the largest rectangle in the histogram
            res = Math.max(res , largestRectangle(height));
        }
        return res;
    }
    
    // Helper function to find the largest rectangle in a histogram
    private static int largestRectangle(int[] height){
        Stack<Integer> stack = new Stack<>();
        int res = 0;
        // Add a sentinel value at the end
        int[] temp = Arrays.copyOf(height , height.length + 1);
        
        for(int i=0;i<temp.length ;i++){
            while(!stack.isEmpty() && temp[i] < temp[stack.peek()]){
                int h = temp[stack.pop()];
                int w = stack.isEmpty() ? i : i - stack.peek() - 1;
                res = Math.max(res , h * w);
            }
            stack.push(i);
        }
        return res;
    }
}
```

---

✨ **Tip:**  
The histogram approach is much faster for large grids and is commonly used in competitive programming for this problem.
