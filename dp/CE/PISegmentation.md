# 🧩 Problem Statement:

You are given a string representing the first `n` digits of **π (pi)**. You also have a **dictionary** of strings, where each string is a valid number.

Your task is to **insert the minimum number of spaces** into the pi string so that each resulting segment exists in the dictionary.

* You can reuse dictionary entries multiple times.
* Each segment after inserting spaces must **exactly match** a string in the dictionary.
* If it's impossible to segment the entire pi string, return `-1`.

---

## 📥 Input Format:

```
Line 1: A string `pi` consisting of digits (no spaces).
Line 2: An integer `N` — the number of dictionary entries.
Next N lines: Each line contains a string representing a valid number.
```

## 📤 Output Format:

```
Print the **minimum number of spaces** inserted to segment the pi string.
If not possible, print `-1`.
```

---

## ✅ Sample Input 1:

```
3141
3
1
3
4
```

### ✅ Output 1:

```
3
```

### 🔍 Explanation:

We can split the string as: `3 | 1 | 4 | 1`
All segments exist in the dictionary: ✅
We inserted **3** spaces.

---

## ✅ Sample Input 2:

```
314159
5
3
1
4
15
9
```

### ✅ Output 2:

```
4
```

### 🔍 Explanation:

Split: `3 | 1 | 4 | 15 | 9`
4 spaces inserted → Valid segments ✅
Answer: **4**

---

## ❌ Sample Input 3 (No valid segmentation):

```
314
2
2
9
```

### ✅ Output:

```
-1
```

### 🔍 Explanation:

No way to split `314` into segments from `{2, 9}`. ❌

---


## ✅ Top-Down DP with Memoization (Original Code - Unchanged)

```java
import java.util.*;

class PISegmentation {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String pi = sc.nextLine();
        int n = Integer.parseInt(sc.nextLine());
        Set<String> dict = new HashSet<>();
        for (int i = 0; i < n; i++) {
            dict.add(sc.nextLine());
        }

        int[] memo = new int[pi.length()];
        Arrays.fill(memo, Integer.MAX_VALUE);

        int space = getSpaces(pi, dict, memo, 0, pi.length());
        System.out.println(space != Integer.MAX_VALUE ? space : -1);
    }

    private static int getSpaces(String pi, Set<String> dict, int[] memo, int index, int n) {
        if (index == n) return -1; // no space needed at the end
        if (memo[index] != Integer.MAX_VALUE) return memo[index];

        int minSpaces = Integer.MAX_VALUE;

        for (int i = index + 1; i <= n; i++) {
            if (dict.contains(pi.substring(index, i))) {
                int next = getSpaces(pi, dict, memo, i, n);
                if (next != Integer.MAX_VALUE) {
                    minSpaces = Math.min(minSpaces, next + 1);
                }
            }
        }

        return memo[index] = minSpaces;
    }
}
```

---

## ✅ Bottom-Up DP (Tabulation) — Original Code (Unchanged)

```java
import java.util.*;

class PISegmentation {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String pi = sc.nextLine();
        int n = Integer.parseInt(sc.nextLine());
        Set<String> dict = new HashSet<>();
        for (int i = 0; i < n; i++) {
            dict.add(sc.nextLine());
        }

        int space = getSpaces(pi, dict);
        System.out.println(space != Integer.MAX_VALUE ? space : -1);
    }

    private static int getSpaces(String pi, Set<String> dict) {
        int n = pi.length();
        int[] dp = new int[n + 1];
        Arrays.fill(dp, Integer.MAX_VALUE);
        dp[0] = -1;

        for (int i = 1; i <= n; i++) {
            for (int j = 0; j < i; j++) {
                if (dict.contains(pi.substring(j, i))) {
                    if (dp[j] != Integer.MAX_VALUE) {
                        dp[i] = Math.min(dp[i], dp[j] + 1);
                    }
                }
            }
        }

        return dp[n];
    }
}
```

---

## 🧠 Time and Space Complexity:

| Metric            | Top-Down                    | Bottom-Up        |
| ----------------- | --------------------------- | ---------------- |
| Time Complexity   | O(n × 10) = O(n)            | O(n × 10) = O(n) |
| Space Complexity  | O(n) + O(n) recursion stack | O(n)             |
| Dictionary lookup | O(1) using HashSet          | O(1)             |

> Where `n = pi.length()`, and `10` is max segment length.

---