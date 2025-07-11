# 🧩 Problem Statement

You are given:

* `numDice`: number of standard dice.
* `numSides`: number of faces (sides) on each die.
* `target`: desired total sum from all dice rolls.

### 🎯 Goal:

Calculate the total **number of permutations** of rolls such that the **sum equals the target**.

> Each die can roll values from **1 to numSides**.
> Order **matters**: `[2,3]` ≠ `[3,2]`.
> Use **Dynamic Programming** for efficiency.

---

## ✅ Input Format

```
Line 1: Integer numDice → number of dice  
Line 2: Integer numSides → sides per die  
Line 3: Integer target → target sum to achieve
```

---

## ✅ Output Format

```
Single integer → number of permutations where sum = target
```

---

## ✅ Constraints

* 1 ≤ numDice ≤ 30
* 1 ≤ numSides ≤ 30
* 1 ≤ target ≤ 1000

---

## ✅ Sample Input 1

```
1
6
3
```

### ✅ Output 1

```
1
```

### ✅ Explanation:

One die can roll 1 to 6. Only one way to get 3: `[3]`

---

## ✅ Sample Input 2

```
2
6
7
```

### ✅ Output 2

```
6
```

### ✅ Explanation:

All permutations of two dice that sum to 7 are:
`[1,6], [2,5], [3,4], [4,3], [5,2], [6,1]` → 6 permutations.

---

## ✅ Java Code (Unchanged) — With Comments

```java
import java.util.*;

class Dice {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int dice = sc.nextInt();   // Number of dice
        int sides = sc.nextInt();  // Sides per die
        int target = sc.nextInt(); // Target sum

        // dp[t] = number of ways to reach sum t
        int[] dp = new int[target + 1];
        dp[0] = 1;  // Base case: one way to get 0 with 0 dice

        // Loop through all dice
        for (int i = 1; i <= dice; i++) {
            int[] newdp = new int[target + 1];

            // For each target sum from 1 to target
            for (int t = 1; t <= target; t++) {

                // Try all face values from 1 to sides
                for (int f = 1; f <= sides; f++) {
                    if (f <= t) {
                        // Add ways to reach (t - f) using previous dice
                        newdp[t] += dp[t - f];
                    }
                }
            }

            // Move to next dice level
            dp = newdp;
        }

        // Result: number of permutations to reach target using all dice
        System.out.println(dp[target]);
    }
}
```

---

## 🧠 Time & Space Complexity

| Aspect | Complexity                               |
| ------ | ---------------------------------------- |
| Time   | O(numDice × target × numSides)           |
| Space  | O(target) → 1D DP array reused per level |

> Efficient enough for constraints (up to 30 dice and target up to 1000)

---
