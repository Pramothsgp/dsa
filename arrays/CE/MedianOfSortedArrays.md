# Median of Two Sorted Arrays

Given two sorted arrays, `nums1` and `nums2`, of size `m` and `n` respectively, return the median of the two sorted arrays.

The overall run time complexity should be **O(log (m+n))**.

---

## Example 1

**Input:**  
nums1 = 1 3 (size = 2), nums2 = 2 (size = 1)

**Output:**  
2.00

**Explanation:**  
Merged array = [1, 2, 3] and median is 2.

---

## Example 2

**Input:**  
nums1 = 1 2 (size = 2), nums2 = 3 4 (size = 2)

**Output:**  
2.50

**Explanation:**  
Merged array = [1, 2, 3, 4] and median is (2 + 3) / 2 = 2.5.

---

## Input Format

- The first line of input consists of an integer `m`, representing the number of elements in the first sorted array, `nums1`.
- The second line consists of `m` space-separated integers, representing the elements of `nums1` in sorted order.
- The third line consists of an integer `n`, representing the number of elements in the second sorted array `nums2`.
- The fourth line consists of `n` space-separated integers, representing the elements of `nums2` in sorted order.

## Output Format

- The output prints a single floating-point value (up to 2 decimal places), representing the median of the merged sorted array formed from `nums1` and `nums2`.

Refer to the sample output for formatting specifications.

---

## Code Constraints

- `nums1.length == m`
- `nums2.length == n`
- `0 ≤ m ≤ 1000`
- `0 ≤ n ≤ 1000`
- `1 ≤ m + n ≤ 2000`
- `-10^6 ≤ nums1[i], nums2[i] ≤ 10^6`

---

## Sample Test Cases

**Input 1:**
```
2
1 3
1
2
```
**Output 1:**
```
2.00
```

**Input 2:**
```
2
1 2
2
3 4
```
**Output 2:**
```
2.50
```

---

## Java Implementation

```java
import java.util.*;

class Median {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // Read the size of the first array
        int n = sc.nextInt();
        int[] nums1 = new int[n];

        // Read elements of the first array
        for (int i = 0; i < n; i++) {
            nums1[i] = sc.nextInt();
        }

        // Read the size of the second array
        int m = sc.nextInt();
        int[] nums2 = new int[m];

        // Read elements of the second array
        for (int i = 0; i < m; i++) {
            nums2[i] = sc.nextInt();
        }

        // Print the median with 2 decimal places
        System.out.printf("%.2f", median(nums1, nums2));
    }

    // Function to find the median of two sorted arrays
    private static double median(int[] nums1, int[] nums2) {
        int n = nums1.length;
        int m = nums2.length;
        int i = 0, j = 0, m1 = -1, m2 = -1;

        // Iterate to the middle of the merged array
        for (int k = 0; k <= (n + m) / 2; k++) {
            m2 = m1;
            if (i != n && j != m) {
                // Choose the smaller value from both arrays
                m1 = (nums1[i] > nums2[j]) ? nums2[j++] : nums1[i++];
            } else if (i < n) {
                // If elements remain in nums1
                m1 = nums1[i++];
            } else {
                // If elements remain in nums2
                m1 = nums2[j++];
            }
        }

        // If total number of elements is even, return average of two middle values
        // Otherwise, return the middle value
        return (n + m) % 2 == 0 ? (m1 + m2) / 2d : m1;
    }
}
```