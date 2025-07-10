# Longest Strict Bitonic Subsequence
## 🧩 **Problem Statement**

Given an array of integers, the task is to find the **length of the longest strict bitonic subsequence**.
A **bitonic subsequence** is defined as a subsequence that is:

* Strictly increasing and then strictly decreasing, **or**
* Strictly decreasing.

---

### 📥 Input Format

* The first line contains an integer `n` – the size of the array.
* The second line contains `n` space-separated integers – the elements of the array.

---

### 📤 Output Format

* Print:
  `"Longest length strict bitonic subsequence = X"`
  Where `X` is the length of the longest strict bitonic subsequence.

---

### 🔒 Constraints

* 1 ≤ n ≤ 10
* 1 ≤ arr\[i] ≤ 50

---

### 🧪 Sample Input/Output

**Input 1:**

```
8
1 5 2 3 4 5 3 2
```

**Output 1:**

```
Longest length strict bitonic subsequence = 6
```

**Input 2:**

```
9
1 2 5 3 6 7 4 6 5
```

**Output 2:**

```
Longest length strict bitonic subsequence = 5
```

---

### ✅ Code

```java
import java.util.*;

class LongestBitonicSubSequence {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        
        // Input size of array
        int n = sc.nextInt();
        int[] nums = new int[n];

        // Input array elements
        for (int i = 0; i < n; i++) {
            nums[i] = sc.nextInt();
        }

        // Output result
        System.out.printf("Longest length strict bitonic subsequence = %d", lbs(nums));
    }

    private static int lbs(int[] nums) {
        int n = nums.length;
        int i, j;

        // Compute Longest Increasing Subsequence with adjacent diff = 1
        int[] lis = new int[n];
        Arrays.fill(lis, 1);
        for (i = 1; i < n; i++) {
            for (j = 0; j < i; j++) {
                if (nums[i] > nums[j] && Math.abs(nums[i] - nums[j]) == 1 && lis[i] < lis[j] + 1) {
                    lis[i] = lis[j] + 1;
                }
            }
        }

        // Compute Longest Decreasing Subsequence with adjacent diff = 1
        int[] lds = new int[n];
        Arrays.fill(lds, 1);
        for (i = n - 2; i >= 0; i--) {
            for (j = n - 1; j > i; j--) {
                if (nums[i] > nums[j] && Math.abs(nums[i] - nums[j]) == 1 && lds[i] < lds[j] + 1) {
                    lds[i] = lds[j] + 1;
                }
            }
        }

        // Find maximum length of bitonic subsequence
        int res = lis[0] + lds[0] - 1;
        for (i = 1; i < n; i++) {
            res = Math.max(res, lis[i] + lds[i] - 1);
        }

        return res;
    }
}
```

