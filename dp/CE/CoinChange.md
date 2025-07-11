# 📄 Problem Statement

**Vijay** runs a shop where he only accepts coins of specific denominations. He needs to give exact change to customers using **an unlimited supply** of these coins.

You are to help Vijay by writing a function to determine:

> 🧮 **How many different combinations** of coins can sum up to the required amount?

---

## 📥 Input Format

1. Integer `n` — number of coin denominations
2. `n` space-separated positive integers — distinct coin denominations
3. Integer `amount` — the total amount of change to make

---

## 📤 Output Format

* Single integer — total number of **distinct combinations** of coins that sum up to the given amount

---

## 💡 Sample Input/Output

### 🔹 Input 1:

```
7
1 6 7 9 2 2 5
5
```

**Output:**

```
7
```

### 🔹 Input 2:

```
4
1 2 3 4
10
```

**Output:**

```
23
```

---

## ✅ Java Code (Formatted & Documented)

```java
import java.util.*;

class CoinChange {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // Step 1: Read number of coin denominations
        int n = sc.nextInt();
        int[] coins = new int[n];

        // Step 2: Read each coin denomination
        for (int i = 0; i < n; i++) {
            coins[i] = sc.nextInt();
        }

        // Step 3: Read the target amount to make
        int target = sc.nextInt();

        // Step 4: Call the function and print the result
        System.out.println(coinChange(coins, target));
    }

    // Function to calculate number of combinations to make 'target' using given coins
    private static int coinChange(int[] coins, int target) {
        // dp[i] will store number of combinations to make sum 'i'
        int[] dp = new int[target + 1];

        // Base case: One way to make sum = 0 → use no coins
        dp[0] = 1;

        // Step 5: For each coin, update combinations for all amounts from coin to target
        for (int coin : coins) {
            for (int i = coin; i <= target; i++) {
                dp[i] += dp[i - coin];
                // Explanation:
                // If we know how to make (i - coin), then by adding this coin,
                // we can make 'i' as well.
            }
        }

        // Return the total combinations for the target amount
        return dp[target];
    }
}
```

---

## 🧠 Explanation

We use **Dynamic Programming**:

* `dp[i]` stores the number of ways to make sum `i`.
* Start with `dp[0] = 1` (1 way to make amount 0 → by using no coins).
* For each coin, we update `dp[i]` by adding `dp[i - coin]`.

💡 This ensures **combinations are counted**, not permutations.

---

## ⏱️ Time & Space Complexity

| Metric               | Value           |
| -------------------- | --------------- |
| **Time Complexity**  | `O(n * amount)` |
| **Space Complexity** | `O(amount)`     |

---
