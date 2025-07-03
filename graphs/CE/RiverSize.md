## 🌊 River Size Problem

> **Aarav**, a geography student, analyzes satellite images represented as a 2D binary matrix:

- **`1`**: River cell  
- **`0`**: Land cell

**Rivers** are groups of horizontally or vertically connected `1`s (no diagonal connections). Each river can twist in any shape, as long as its cells are adjacent.

---

### 🎯 **Your Task**

**Find all distinct rivers and output their sizes.**  
<sub>Order of sizes doesn't matter.</sub>

---

### 📝 **Input Format**

1. **First line:** Two integers — number of rows and columns.
2. **Next rows:** Each line contains space-separated `0` or `1` values.

---

### 🖨️ **Output Format**

- Print river sizes (space-separated) in any order.

---

### 📚 **Constraints**

- `1 ≤ rows, cols ≤ 1000`
- Each cell is `0` or `1`
- At most `rows * cols` river cells

---

### 🧪 **Sample Test Cases**

#### **Input 1**
```plaintext
3 3
1 0 0
0 0 0
0 0 1
```
**Output 1**
```plaintext
1 1
```

---

#### **Input 2**
```plaintext
4 4
1 0 0 1
1 1 0 0
0 0 1 0
1 0 1 1
```
**Output 2**
```plaintext
3 1 3 1
```

---

## 🚀 Java Solution

<details>
<summary>Click to expand Java code</summary>

```java
import java.util.*;

class Rivers {
    static int[][] graph;
    // Directions: right, down, left, up
    static final int[][] dir = {{0,1},{1,0},{0,-1},{-1,0}};
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int m = sc.nextInt(); // rows
        int n = sc.nextInt(); // columns
        graph = new int[m][n];
        for(int i=0;i<m;i++)
            for(int j=0;j<n;j++)
                graph[i][j] = sc.nextInt();

        List<Integer> res = new ArrayList<>();
        for(int i=0;i<m;i++)
            for(int j=0;j<n;j++)
                if(graph[i][j] == 1)
                    res.add(dfs(i, j));
        System.out.println(res.toString().replaceAll("\\[|\\]|,", ""));
    }

    // DFS to calculate river size
    private static int dfs(int i, int j){
        if(!isValid(i, j)) return 0;
        int size = 0;
        graph[i][j] = 0; // Mark visited
        for(int[] d : dir)
            size += dfs(i + d[0], j + d[1]);
        return size + 1;
    }

    // Check bounds and river cell
    private static boolean isValid(int i, int j){
        return i >= 0 && j >= 0 && i < graph.length && graph[i][j] == 1;
    }
}
```
</details>

---

> 💡 **Tip:** Try implementing the solution in your favorite language!
