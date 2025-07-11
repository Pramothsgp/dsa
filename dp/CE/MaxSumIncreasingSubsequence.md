# 📄 Problem Statement

**Aarav** is analyzing his company's profits over a period, represented as an array of integers. Each element represents the **profit or loss** for a particular month.

He is interested in identifying a **strictly increasing subsequence** of months where profits rise and result in the **maximum total gain**.

Your task is to write a program to determine:

1. 🔸 The **maximum sum** of any strictly increasing subsequence
2. 🔸 The **subsequence itself** (preserving the original order)

---

## 📥 Input Format

* First line: Integer `n` — number of months (1 ≤ n ≤ 1000)
* Second line: `n` space-separated integers representing profits/losses for each month (−10⁴ ≤ a\[i] ≤ 10⁴)

---

## 📤 Output Format

* First line: Integer — the maximum sum of a strictly increasing subsequence
* Second line: The subsequence itself (space-separated, in original order)

---

## 💡 Sample Input & Output

### 🔹 Sample 1

**Input:**

```
4
1 3 4 5
```

**Output:**

```
13
1 3 4 5
```

### 🔹 Sample 2

**Input:**

```
8
10 5 4 3 15 20 8 9
```

**Output:**

```
45
10 15 20
```

---

## 🔍 Explanation

* In **Sample 1**, all elements are increasing → `1 + 3 + 4 + 5 = 13`
* In **Sample 2**, one optimal increasing path is `10 → 15 → 20` → `sum = 45`
  Other increasing subsequences exist, but none with higher sum.

---

## ✅ Java Code (Well-Formatted & Commented)

```java
import java.util.*;

public class LongestIncreasingSubsequenceSum {

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // Step 1: Read the number of months
        int n = sc.nextInt();
        int[] nums = new int[n];

        // Step 2: Read profit/loss for each month
        for (int i = 0; i < n; i++) {
            nums[i] = sc.nextInt();
        }

        // dp[i] = max sum of increasing subsequence ending at index i
        int[] dp = new int[n];

        // prev[i] = index of previous element in the subsequence
        int[] prev = new int[n];
        Arrays.fill(prev, -1);  // Initially, no parent for any element

        int maxIndex = 0;  // Index where the max sum ends

        // Step 3: Dynamic Programming to build dp and prev arrays
        for (int i = 0; i < n; i++) {
            dp[i] = nums[i]; // Base case: single element sequence

            for (int j = 0; j < i; j++) {
                // Check if we can extend increasing subsequence
                if (nums[j] < nums[i] && dp[i] < dp[j] + nums[i]) {
                    dp[i] = dp[j] + nums[i];  // Update max sum ending at i
                    prev[i] = j;              // Remember path
                }
            }

            // Track the index where maximum sum occurs
            if (dp[i] > dp[maxIndex]) {
                maxIndex = i;
            }
        }

        // Step 4: Reconstruct the subsequence using prev[] array
        Stack<Integer> sequence = new Stack<>();
        int index = maxIndex;

        while (index != -1) {
            sequence.push(nums[index]);
            index = prev[index];
        }

        // Step 5: Print the results
        System.out.println(dp[maxIndex]); // Print max sum

        // Print subsequence in correct order
        while (!sequence.isEmpty()) {
            System.out.print(sequence.pop() + " ");
        }
    }
}
```

---

## ⏱️ Time & Space Complexity

| Metric               | Value    |
| -------------------- | -------- |
| **Time Complexity**  | `O(n^2)` |
| **Space Complexity** | `O(n)`   |

* We use two arrays of size `n` for `dp[]` and `prev[]`
* Nested loop results in `O(n^2)` comparisons

---
