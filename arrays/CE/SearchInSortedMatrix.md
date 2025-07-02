# Search a 2D Matrix

You are given an `m x n` integer matrix `matrix` with the following two properties:

- Each row is sorted in non-decreasing order.
- The first integer of each row is greater than the last integer of the previous row.

Given an integer `target`, return `true` if the target is in the matrix or `false` otherwise.

You must write a solution with an **O(log(m\*n))** time complexity.

---

## Example 1

**Input:**
```
matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]]
target = 3
```
**Output:**
```
true
```

## Example 2

**Input:**
```
matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]]
target = 13
```
**Output:**
```
false
```

---

## Input Format

- The first line of input contains a 2D matrix represented as a nested array of integers.
- The second line of input contains an integer representing the target to search for.

## Output Format

- The output prints a boolean value `true` if the target exists in the matrix, otherwise `false`.

Refer to the sample output for formatting specifications.

---

## Code Constraints

- `m == matrix.length`
- `n == matrix[i].length`
- `1 ≤ m, n ≤ 100`
- `-10^4 ≤ matrix[i][j], target ≤ 10^4`

---

## Python
``` py []
import ast
def searchMatrix(matrix, target):
    m, n = len(matrix), len(matrix[0])
    left, right = 0, m * n - 1
    while left <= right:
        mid = (left + right) // 2
        row, col = divmod(mid, n)
        if matrix[row][col] == target:
            return True
        elif matrix[row][col] < target:
            left = mid + 1
        else:
            right = mid - 1
    return False

def main():
    matrix = ast.literal_eval(input())
    target = int(input())
    print(str(searchMatrix(matrix, target)).lower())

main()
```

## Java

```java []
import java.util.*;

public class MatrixSearch {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String[] s = sc.nextLine().replaceAll("\\[\\[|\\]\\]", "").split("\\],\\[");
        int[][] matrix = new int[s.length][];
        for (int i = 0; i < s.length; i++) {
            String[] row = s[i].split(",");
            matrix[i] = new int[row.length];
            for (int j = 0; j < row.length; j++) {
                matrix[i][j] = Integer.parseInt(row[j]);
            }
        }
        int target = sc.nextInt();
        System.out.println(searchMatrix(matrix, target));
    }

    // Binary Search
    private static boolean searchMatrix(int[][] matrix, int target) {
        int m = matrix.length, n = matrix[0].length;
        int left = 0, right = m * n - 1;
        while (left <= right) {
            int mid = left + (right - left) / 2;
            int row = mid / n, col = mid % n;
            if (matrix[row][col] == target) {
                return true;
            } else if (matrix[row][col] < target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        return false;
    }

    // Staircase Search
    public boolean searchMatrix(int[][] grid, int target) {
        int n = grid.length , m = grid[0].length;
        int i =0 , j = m - 1;
        while(i < n && j >=0 ){
            if(target > grid[i][j]){
                i++;
            } else if(target < grid[i][j]){
                j--;
            } else {
                return true;
            }
        }
        return false;
    }
}
```


