
# 🏃‍♂️ Jump Game II – Single File Java Program

---

## 📝 Problem Statement

You're given a **0-indexed** array of integers `nums` of length `n`.

Each element `nums[i]` represents the **maximum jump length** you can make from index `i`.

Your goal is to return the **minimum number of jumps** required to reach the **last index**.

> It's guaranteed that you can always reach the last index.

---

## 📥 Input Format

* A single line containing **space-separated integers** representing jump lengths.

## 📤 Output Format

* A single integer: the **minimum number of jumps** to reach the end.

---

## 📌 Constraints

* `1 ≤ nums.length ≤ 10^4`
* `0 ≤ nums[i] ≤ 1000`
* It is guaranteed you can always reach the last index.

---

## 🧪 Sample Test Cases

### Input 1:

```
2 3 1 1 4
```

### Output 1:

```
2
```

### Input 2:

```
2 3 0 1 4
```

### Output 2:

```
2
```

---

## 💡 Explanation

### Example 1:

* Start at index `0` with value `2`.
  → You can jump to index `1` or `2`.
* Choose index `1` (value = 3), now you can jump directly to the end.
  ✅ Total jumps = **2**

---

## ✅ Java Code – O(N) Greedy Approach

```java
import java.util.*;

class Jumps {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // Read and parse the input array
        String[] s = sc.nextLine().split("\\s+");
        int n = s.length;
        int[] nums = new int[n];
        for (int i = 0; i < n; i++) {
            nums[i] = Integer.parseInt(s[i]);
        }

        // Initialize the variables
        int jumps = 0;       // Count of jumps taken
        int end = 0;         // Current farthest reachable index in the current jump
        int farthest = 0;    // Maximum reachable index in the next jump

        // Traverse up to the second-last index
        for (int i = 0; i < n - 1; i++) {
            // Update the farthest index reachable from current position
            farthest = Math.max(farthest, i + nums[i]);

            // If we have come to the end of the current jump's range
            if (i == end) {
                jumps++;       // Take a jump
                end = farthest; // Update end to the new farthest
            }
        }

        // Output the result
        System.out.println(jumps);
    }
}
```

---

## ⏱ Time & Space Complexity

| Metric           | Value                                      |
| ---------------- | ------------------------------------------ |
| Time Complexity  | O(N)                                       |
| Space Complexity | O(N) for input parsing, O(1) after parsing |

---

✅ This is the optimal greedy solution that runs in linear time and doesn't require extra DP arrays.
