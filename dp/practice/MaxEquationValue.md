# 🧩 Problem Statement

You’re given an integer array `nums`. You need to **compute the maximum value** of the expression:

```
nums[a] - nums[b] + nums[c] - nums[d]
```

with the constraint:

```
a < b < c < d
```

That is, you must pick 4 **strictly increasing indices**.

---

## ✅ Input Format

```
Line 1: Integer n — number of elements in array  
Line 2: n space-separated integers — the array elements
```

---

## ✅ Output Format

```
Single integer — maximum value of the expression: nums[a] - nums[b] + nums[c] - nums[d]
```

---

## ✅ Constraints

* 4 ≤ n ≤ 10⁵
* -10⁴ ≤ nums\[i] ≤ 10⁴
* Time Complexity: O(n)

---

## 🧠 Strategy (Dynamic Programming)

We'll calculate step-by-step:

* `a = max(nums[0..i])`
* `b = max(a - nums[j])`
* `c = max(b + nums[k])`
* `res = max(c - nums[l])`

We'll keep **updating** the max value of each expression as we move through the array.

This is done in **a single O(n) pass**, storing only 4 variables.

---

## ✅ Sample Input 1

```
5
1 2 3 4 5
```

## ✅ Output 1

```
-2
```

### 🔍 Explanation:

Let's manually test possible (a, b, c, d) combinations:

* (0,1,2,3): 1-2+3-4 = -2
* (0,1,2,4): 1-2+3-5 = -3
* ...
* Max is `-2`

---

## ✅ Sample Input 2

```
8
3 1 6 2 8 4 9 0
```

## ✅ Output 2

```
13
```

### 🔍 Explanation:

Best combination is (0,1,4,7):
`nums[0] - nums[1] + nums[4] - nums[7] = 3 - 1 + 8 - 0 = 10`
Actually, (2,3,6,7) → 6 - 2 + 9 - 0 = **13** → max

---

## ✅ Final Java Code (UNCHANGED) — With Comments

```java
import java.util.*;

class MaxExuationValue {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // Step 1: Read input
        int n = sc.nextInt();
        int[] nums = new int[n];
        for(int i = 0; i < n; i++) {
            nums[i] = sc.nextInt();
        }

        // Edge case: If less than 4 elements, no valid a < b < c < d
        if (n < 4) {
            System.out.println(0);
            return;
        }

        // Step 2: Initialize values
        int a = nums[0];                 // max of nums[a]
        int b = Integer.MIN_VALUE;       // max of nums[a] - nums[b]
        int c = Integer.MIN_VALUE;       // max of nums[a] - nums[b] + nums[c]
        int res = Integer.MIN_VALUE;     // max of expression

        // Step 3: Traverse the array
        for(int i = 0; i < n; i++) {
            if(i >= 3) {
                res = Math.max(res, c - nums[i]);          // Evaluate full expression
            }

            if(i >= 2) {
                c = Math.max(c, b + nums[i]);              // max of a - b + c
            }

            if(i >= 1) {
                b = Math.max(b, a - nums[i]);              // max of a - b
            }

            a = Math.max(a, nums[i]);                      // max of a
        }

        // Step 4: Print result
        System.out.println(res);
    }
}
```

---

## 💡 Time & Space Complexity

| Aspect           | Value                                        |
| ---------------- | -------------------------------------------- |
| Time Complexity  | **O(n)**                                     |
| Space Complexity | **O(1)** (no extra space except 4 variables) |

---
