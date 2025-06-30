Set Matrix Zeros

---

Given an m x n integer matrix `matrix`, if an element is 0, set its entire row and column to 0's.

You must do it in place.

---

### Example 1

![Example 1](https://assets.leetcode.com/uploads/2020/08/17/mat1.jpg)

**Input:**  
`matrix = [[1,1,1],[1,0,1],[1,1,1]]`

**Output:**  
`[[1,0,1],[0,0,0],[1,0,1]]`

---

### Example 2

![Example 2](https://assets.leetcode.com/uploads/2020/08/17/mat2.jpg)

**Input:**  
`matrix = [[0,1,2,0],[3,4,5,2],[1,3,1,5]]`

**Output:**  
`[[0,0,0,0],[0,4,5,0],[0,3,1,0]]`

---

**Input format:**  
The input contains a 2D array represented as a nested array of integers.

**Output format:**  
The output prints a 2D matrix representing the modified matrix after applying the algorithm that sets entire rows and columns to zero wherever a zero is found in the original matrix.

Refer to the sample output for formatting specifications.

---

**Code constraints:**
- The number of rows will be between 1 and 10.
- The number of columns will be between 1 and 10.
- The matrix will contain integers where 0 represents a contaminated room, and other values represent sanitized rooms.
---
## Python
```python []
import ast

def main():
    grid = ast.literal_eval(input())
    # Flags to check if first row or first column need to be zeroed
    row , col = False , False
    n , m = len(grid) , len(grid[0])
    # Check if any element in the first row is zero
    for i in grid[0]:
        if i == 0:
            row = True
            break
    # Check if any element in the first column is zero
    for i in range(n):
        if grid[i][0] == 0:
            col = True
            break
        
    # Use first row and column as markers for zeroing
    for i in range(1 , n):
        for j in range(1 , m):
            if(grid[i][j] == 0):
                grid[i][0] = 0
                grid[0][j] = 0
                
    # Set matrix cells to zero based on markers
    for i in range(1 , n):
        for j in range(1 , m):
            if grid[i][0] == 0 or grid[0][j] == 0:
                grid[i][j] = 0
                
    # Zero out the first row if needed
    if row:
        for j in range(m):
            grid[0][j] = 0
    
    # Zero out the first column if needed
    if col:
        for i in range(n):
            grid[i][0] = 0
            
    # Print the modified grid in the required format
    print(str(grid).replace(" " , ""))
    
main()
```