## Problem Statement

Given an array of points where `points[i] = [xi, yi]` represents a point on the X-Y plane, return the maximum number of points that lie on the same straight line.

### Example 1

**Input:**  
`points = [[1,1],[2,2],[3,3]]`  
**Output:**  
`3`

### Example 2

**Input:**  
`points = [[1,1],[3,2],[5,3],[4,1],[2,3],[1,4]]`  
**Output:**  
`4`

---

### Input format

- The first line contains an integer `n`, representing the number of points.
- The next `n` lines each contain two space-separated integers `xi` and `yi`, representing the x and y coordinates of the i-th point.

### Output format

- The output prints an integer, representing the maximum number of points that lie on the same straight line.

Refer to the sample output for the formatting specifications.

---

### Code constraints

- `1 ≤ n ≤ 20`
- `points[i].length == 2`
- `1 ≤ xi, yi ≤ 102`

---

### Sample test cases

**Input 1:**
```
6
1 1
3 2
5 3
4 1
2 3
1 4
```
**Output 1:**
```
4
```

**Input 2:**
```
3
1 1
2 2
3 3
```
**Output 2:**
```
3
```

---

```java
import java.util.*;

class Graph {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[][] points = new int[n][2];
        // Read all points from input
        for (int i = 0; i < n; i++) {
            points[i][0] = sc.nextInt();
            points[i][1] = sc.nextInt();
        }
        System.out.println(colinearPoints(points));
    }

    // Function to find the maximum number of colinear points
    private static int colinearPoints(int[][] points) {
        int n = points.length;
        if (n <= 2) return n; // If 2 or fewer points, all are colinear
        int res = 0;

        // Iterate through each point
        for (int i = 0; i < n; i++) {
            int duplicates = 1; // Count of duplicate points
            Map<String, Integer> slopes = new HashMap<>(); // Map to store slopes

            // Compare with every other point
            for (int j = i + 1; j < n; j++) {
                // If points are identical, increment duplicates
                if (points[i][0] == points[j][0] && points[i][1] == points[j][1]) {
                    duplicates++;
                    continue;
                }
                int dx = points[i][0] - points[j][0];
                int dy = points[i][1] - points[j][1];

                String slop;
                // Handle vertical and horizontal lines
                if (dx == 0) {
                    slop = "v";
                } else if (dy == 0) {
                    slop = "h";
                } else {
                    int divisor = gcd(dx, dy);
                    slop = (dx / divisor) + "/" + (dy / divisor);
                }
                // Count points with the same slope
                slopes.put(slop, slopes.getOrDefault(slop, 0) + 1);
            }

            // If all points are duplicates
            if (slopes.isEmpty()) {
                res = Math.max(res, duplicates);
            } else {
                int max = 0;
                // Find the maximum number of points with the same slope
                for (int val : slopes.values()) {
                    max = Math.max(max, val);
                }
                res = Math.max(res, max);
            }
        }
        // Add 1 to include the starting point itself
        return res + 1;
    }

    // Helper function to compute GCD
    private static int gcd(int a, int b) {
        return a == 0 ? b : gcd(b % a, a);
    }
}
```