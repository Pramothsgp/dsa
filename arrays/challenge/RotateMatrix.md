# Rotate Image

You are given an n x n 2D matrix representing an image, rotate the image by 90 degrees (clockwise).

You have to rotate the image in-place, which means you have to modify the input 2D matrix directly. **DO NOT** allocate another 2D matrix and do the rotation.

![Sample Image 1](https://s3.amazonaws.com/exams-media-content/041909ab-d1f3-4165-98a9-a513d85388b9/questions/2675902989-1)

**Input:**  
`matrix = [[1,2,3],[4,5,6],[7,8,9]]`

**Output:**  
`[[7,4,1],[8,5,2],[9,6,3]]`

![Sample Image 2](https://s3.amazonaws.com/exams-media-content/041909ab-d1f3-4165-98a9-a513d85388b9/questions/2675902989-2)

**Input:**  
`matrix = [[5,1,9,11],[2,4,8,10],[13,3,6,7],[15,14,12,16]]`

**Output:**  
`[[15,13,2,5],[14,3,4,1],[12,6,8,9],[16,7,10,11]]`

---

### Input format

- The input consists of multiple lines. Each line represents a row of the matrix, and the integers in each row are space-separated.
- The first line represents the first row of the matrix.
- The second line represents the second row of the matrix, and so on.
- Each matrix is an n x n matrix (square matrix).

### Output format

- The output prints the rotated matrix as a 2D array. Each row of the matrix is enclosed in square brackets, and rows are separated by commas.  
    (Example: `[[7, 4, 1], [8, 5, 2], [9, 6, 3]]`)

Refer to the sample output for formatting specifications.

---

### Code constraints

- `n == matrix.length == matrix[i].length`
- `1 ≤ n ≤ 20`
- `-1000 ≤ matrix[i][j] ≤ 1000`

---

### Sample test cases

**Input 1:**
```
1 2 3
4 5 6
7 8 9
```
**Output 1:**  
`[[7, 4, 1], [8, 5, 2], [9, 6, 3]]`

**Input 2:**
```
5 1 9 11
2 4 8 10
13 3 6 7
15 14 12 16
```
**Output 2:**  
`[[15, 13, 2, 5], [14, 3, 4, 1], [12, 6, 8, 9], [16, 7, 10, 11]]`

---

```java
import java.util.*;

class RotateMatrix {
        public static void main(String[] args) {
                Scanner sc = new Scanner(System.in);
                // Read the first row and determine the size of the matrix
                String s[] = sc.nextLine().split(" ");
                int n = s.length;
                int[][] grid = new int[n][n];
                // Fill the first row
                for (int i = 0; i < n; i++) {
                        grid[0][i] = Integer.parseInt(s[i]);
                }
                // Fill the remaining rows
                for (int i = 1; i < n; i++) {
                        for (int j = 0; j < n; j++) {
                                grid[i][j] = sc.nextInt();
                        }
                }

                // Rotate the matrix in-place
                rotate(grid);

                // Format and print the rotated matrix as a 2D array
                StringBuilder sb = new StringBuilder("[");
                for (int i = 0; i < n; i++) {
                        sb.append("[");
                        for (int j = 0; j < n; j++) {
                                sb.append(grid[i][j]);
                                if (j != n - 1) {
                                        sb.append(", ");
                                }
                        }
                        sb.append("]");
                        if (i != n - 1) {
                                sb.append(", ");
                        }
                }
                sb.append("]");

                System.out.println(sb);

        }

        // Rotates the matrix by 90 degrees clockwise in-place
        private static void rotate(int[][] grid) {
                int n = grid.length;

                // Transpose the matrix
                for (int i = 0; i < n; i++) {
                        for (int j = i + 1; j < n; j++) {
                                swap(grid, i, j, j, i);
                        }
                }

                // Reverse each row
                for (int i = 0; i < n; i++) {
                        for (int j = 0; j < n / 2; j++) {
                                swap(grid, i, j, i, n - j - 1);
                        }
                }

        }

        // Swaps two elements in the matrix using XOR swap
        private static void swap(int[][] grid, int i, int j, int x, int y) {
                grid[i][j] = grid[x][y] ^ grid[i][j] ^ (grid[x][y] = grid[i][j]);
        }
}
```