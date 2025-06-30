# Trapping Rain Water

Given `n` non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it can trap after raining.

---

## Example 1

![Elevation Map](https://assets.leetcode.com/uploads/2018/10/22/rainwatertrap.png)

**Input:**  
`height = 0 1 0 2 1 0 1 3 2 1 2 1` (size = 12)

**Output:**  
Amount of trapped water: `6`

**Explanation:**  
The above elevation map (black section) is represented by an array `[0,1,0,2,1,0,1,3,2,1,2,1]`. In this case, 6 units of rainwater (blue section) are being trapped.

---

## Example 2

**Input:**  
`height = 4 2 0 3 2 5` (size = 6)

**Output:**  
`9`

---

## Input format

- The first line of input consists of an integer `n`, representing the number of elements in the elevation map.
- The second line consists of `n` space-separated integers representing the heights of the bars.

## Output format

- The output prints an integer representing the total amount of trapped water.

Refer to the sample output for the formatting specifications.

---

## Code constraints

- `n == height.length`
- `1 ≤ n ≤ 2 * 10^4`
- `0 ≤ height[i] ≤ 10^5`

---

## Sample test cases

**Input 1:**
```
12
0 1 0 2 1 0 1 3 2 1 2 1
```
**Output 1:**
```
6
```

**Input 2:**
```
6
4 2 0 3 2 5
```
**Output 2:**
```
9
```

---

## Java Implementation

```java
import java.util.*;

class TrappingRainWater {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[] height = new int[n];
        for (int i = 0; i < n; i++) {
            height[i] = sc.nextInt(); // Read the height of each bar
        }

        System.out.println(trapWater(height)); // Output the result
    }

    // Function to compute the total trapped water
    private static int trapWater(int[] height) {
        int left = 0, right = height.length - 1; // Initialize pointers
        int leftMax = height[left], rightMax = height[right]; // Track max heights
        int res = 0; // Store result

        while (left < right) {
            if (leftMax < rightMax) {
                leftMax = Math.max(leftMax, height[++left]); // Update leftMax
                res += leftMax - height[left]; // Add trapped water at left
            } else {
                rightMax = Math.max(rightMax, height[--right]); // Update rightMax
                res += rightMax - height[right]; // Add trapped water at right
            }
        }
        return res;
    }
}
```