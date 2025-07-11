# 📦 Problem Statement: 0/1 Knapsack

Arjun, a delivery agent, has a knapsack with a **maximum carrying capacity**. He needs to choose from a set of items — each with a **value** and a **weight** — such that:

* He can select **each item only once**
* The **total weight** does **not exceed** the knapsack’s capacity
* The **total value** is **maximized**

### You need to:

1. Return the **maximum total value** he can carry
2. Return the **indices (0-based)** of the selected items that give this value

---

## 📥 Input Format

1. First line: Integer `n` — number of items
2. Next `n` lines: Two integers per line

   * `value` and `weight` of each item
3. Last line: Integer `capacity` — maximum weight Arjun can carry

---

## 📤 Output Format

1. Maximum total value that can be carried
2. Indices (0-based) of selected items in **increasing order**

---

## 🧪 Sample Test Cases

### Input 1:

```
4
60 10
100 20
120 30
80 40
50
```

**Output:**

```
220
1 2
```

### Input 2:

```
7
10 5
40 4
30 6
50 6
40 5
30 2
90 8
10
```

**Output:**

```
120
5 6
```

---

## ✅ Java Code (Fully Explained)

```java
import java.util.*;

class KnapSack {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // Step 1: Read number of items
        int n = sc.nextInt();

        // Step 2: Read value and weight for each item into 2D array
        int[][] items = new int[n][2]; // items[i][0] = value, items[i][1] = weight
        for (int i = 0; i < n; i++) {
            items[i][0] = sc.nextInt(); // value
            items[i][1] = sc.nextInt(); // weight
        }

        // Step 3: Read the max capacity of the knapsack
        int capacity = sc.nextInt();

        // Step 4: Initialize DP table
        // dp[i][w] = max value using first i items with total weight <= w
        int[][] dp = new int[n + 1][capacity + 1];

        // Step 5: Fill the DP table
        for (int i = 1; i <= n; i++) {
            for (int w = 0; w <= capacity; w++) {
                // If current item's weight <= current capacity
                if (items[i - 1][1] <= w) {
                    // Choose max of excluding or including current item
                    dp[i][w] = Math.max(
                        dp[i - 1][w], // don't take current item
                        dp[i - 1][w - items[i - 1][1]] + items[i - 1][0] // take it
                    );
                } else {
                    dp[i][w] = dp[i - 1][w]; // can't take item (weight too much)
                }
            }
        }

        // Step 6: Backtrack to find which items were chosen
        int w = capacity;
        List<Integer> res = new ArrayList<>();

        for (int i = n; i >= 1; i--) {
            // If value changes from previous row, item was included
            if (dp[i][w] != dp[i - 1][w]) {
                res.add(i - 1); // store 0-based index
                w -= items[i - 1][1]; // reduce capacity by weight of selected item
            }
        }

        // Step 7: Sort selected indices to match required output
        Collections.sort(res);

        // Step 8: Print results
        System.out.println(dp[n][capacity]); // Max total value
        System.out.println(res.toString().replaceAll("\\[|\\]|,", "")); // Indices space-separated
    }
}
```

---

## 🧠 Explanation

We solve the **0/1 Knapsack** using **Dynamic Programming**.

* Each cell `dp[i][w]` tells us the **maximum value** we can achieve by considering the first `i` items and capacity `w`
* We **include or exclude** each item based on whether it improves the total value

We later **backtrack** the table to find **which items were used**, then print the indices in sorted order.

---

## ⏱️ Time & Space Complexity

| Metric               | Value             |
| -------------------- | ----------------- |
| **Time Complexity**  | `O(n * capacity)` |
| **Space Complexity** | `O(n * capacity)` |

---
