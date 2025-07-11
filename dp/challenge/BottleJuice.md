# 🍹 TechVarsity Innovation Challenge – Optimal Juice Bottling Strategy

## 📌 Problem Statement

In this challenge, you're helping a startup beverage company maximize revenue from bottling juice. Here's the setup:

* The company has **`n - 1` units of juice**.
* You're given an array `prices[]` where:

  * `prices[i]` is the price earned for bottling **`i` units**.
  * `prices[0] = 0` (0 units = 0 revenue).
* You must decide how to divide the `n - 1` units into valid bottle sizes such that the **total revenue is maximized**.
* Return the chosen **bottle sizes in ascending order**.

---

## ✅ Constraints

* `2 ≤ n ≤ 100`
* `0 ≤ prices[i] ≤ 10^4`
* Exactly one **unique solution exists** for every test case.
* Bottle sizes can **repeat** (e.g., 2 + 2 = 4).

---

## 📥 Input Format

```
First line: Integer n — total size of price array (juice units = n - 1)
Second line: n space-separated integers — prices[0] to prices[n-1]
```

## 📤 Output Format

```
Space-separated bottle sizes that add up to n - 1 and maximize revenue.
(Printed in ascending order)
```

---

## 🧪 Sample Test Cases

### 🔹 Input 1:

```
5
0 2 3 7 8
```

### ✅ Output 1:

```
1 3
```

---

### 🔹 Input 2:

```
5
0 1 5 8 9
```

### ✅ Output 2:

```
2 2
```

---

## 💡 Explanation

* This is a variant of the **Rod Cutting Problem** using **Dynamic Programming**.
* We're maximizing the revenue `dp[i]` for `i` juice units:

  * For each size `j` from `1` to `i`, try including it and combine with the optimal solution of the remaining `i-j`.
  * Track `prev[i]` → last piece size that gave max revenue for `i`.

---

## 💻 Java Code (Formatted & Commented)

```java
import java.util.*;

class JuiceBottles {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // 🔹 Read the number of price entries (n)
        int n = sc.nextInt();

        // 🔹 Read the prices array (index = quantity, value = price)
        int[] bottles = new int[n];
        for (int i = 0; i < n; i++) {
            bottles[i] = sc.nextInt();
        }

        // 🔹 dp[i] = max revenue using i units of juice
        int[] dp = new int[n];

        // 🔹 prev[i] = last chosen bottle size to get dp[i] revenue
        int[] prev = new int[n];

        // 🔁 Build up dp table from 1 to n-1 juice units
        for (int i = 1; i < n; i++) {
            for (int j = 1; j <= i; j++) {
                if (dp[i] < bottles[j] + dp[i - j]) {
                    dp[i] = bottles[j] + dp[i - j];
                    prev[i] = j;
                }
            }
        }

        // 🔙 Backtrack to find chosen bottle sizes
        List<Integer> res = new ArrayList<>();
        int juice = n - 1;
        while (juice > 0) {
            res.add(prev[juice]);
            juice -= prev[juice];
        }

        // 🔹 Print result in ascending order (as required)
        Collections.sort(res);
        System.out.println(res.toString().replaceAll("\\[|\\]|,", ""));
    }
}
```

---

## 🧠 Summary Table

| Feature      | Description                         |
| ------------ | ----------------------------------- |
| Type         | Dynamic Programming                 |
| Problem      | Maximize revenue using bottle sizes |
| Input        | `n` and `prices[0...n-1]`           |
| Output       | Bottle sizes summing to `n-1`       |
| Output Order | Ascending                           |
| Complexity   | `O(n^2)`                            |
| Guarantees   | Unique solution                     |

---
