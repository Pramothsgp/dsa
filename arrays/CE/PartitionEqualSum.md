# Partition Equal Subset Sum

Given an integer array `nums`, return `true` if you can partition the array into two subsets such that the sum of the elements in both subsets is equal, or `false` otherwise.

---

## Example 1

**Input:**  
n = 4  
nums = [1, 5, 11, 5]

**Output:**  
true

**Explanation:**  
The array can be partitioned as `[1, 5, 5]` and `[11]`.

---

## Example 2

**Input:**  
n = 4  
nums = [1, 2, 3, 5]

**Output:**  
false

**Explanation:**  
The array cannot be partitioned into equal-sum subsets.

---

## Input Format

- The first line of input contains an integer `n`, representing the number of elements in the array.
- The second line contains `n` space-separated integers, representing the elements of the array.

## Output Format

- If a valid partition is found, print `"true"`; otherwise, print `"false"`.

Refer to the sample output for formatting specifications.

---

## Constraints

- 1 ≤ nums.length ≤ 200
- 1 ≤ nums[i] ≤ 100

---

## Sample Test Cases

**Input 1:**

```
4
1 2 3 5
```

**Output 1:**

```
false
```

**Input 2:**

```
4
1 5 11 5
```

**Output 2:**

```
true
```

---

## Java Solutions

### Recursive Solution

```java
import java.util.*;

class Partition {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[] nums = new int[n];
        for (int i = 0; i < n; i++) {
            nums[i] = sc.nextInt();
        }
        int sum = Arrays.stream(nums).sum();

        // If sum is odd or only one element, partition is not possible
        System.out.println(sum % 2 == 1 || n == 1 ? false : part(n - 1, nums, sum / 2));
    }

    // Recursive function to check if subset with given sum exists
    private static boolean part(int i, int[] nums, int sum) {
        if (sum == 0) return true; // Found a subset
        if (i < 0) return false;   // No elements left
        if (nums[i] > sum)
            return part(i - 1, nums, sum); // Skip current element if it's greater than sum

        // Include or exclude current element
        return part(i - 1, nums, sum) || part(i - 1, nums, sum - nums[i]);
    }
}
```

---

### Dynamic Programming Solution

```java
import java.util.*;

class Partition {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[] nums = new int[n];
        for (int i = 0; i < n; i++) {
            nums[i] = sc.nextInt();
        }
        int sum = Arrays.stream(nums).sum();

        // If sum is odd or only one element, partition is not possible
        System.out.println(sum % 2 == 1 || n == 1 ? false : part(n, nums, sum / 2));
    }

    // DP function to check if subset with given sum exists
    private static boolean part(int n, int[] nums, int sum) {
        boolean[][] dp = new boolean[n + 1][sum + 1];

        // Base case: sum 0 is always possible (empty subset)
        for (int i = 0; i <= n; i++) {
            dp[i][0] = true;
        }

        // Build the DP table
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= sum; j++) {
                if (j < nums[i - 1]) {
                    dp[i][j] = dp[i - 1][j]; // Can't include current element
                } else {
                    // Include or exclude current element
                    dp[i][j] = dp[i - 1][j] || dp[i - 1][j - nums[i - 1]];
                }
            }
        }
        return dp[n][sum];
    }
}
```

---

**Note:**

- The recursive solution may lead to a stack overflow for large inputs due to its exponential time complexity.
- The dynamic programming solution is more efficient and suitable for the given constraints.
