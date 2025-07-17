

# ✏️ Edit Distance – Single File Java Program

---

## 📝 Problem Statement

Given two strings `word1` and `word2`, return the **minimum number of operations** required to convert `word1` into `word2`.

Allowed operations:

1. **Insert** a character
2. **Delete** a character
3. **Replace** a character

---

## 📥 Input Format

* A single line containing **two space-separated strings**:
  `word1 word2`

## 📤 Output Format

* A single integer: the **minimum number of operations** to convert `word1` to `word2`

---

## 📌 Constraints

* `0 ≤ word1.length, word2.length ≤ 500`
* Strings consist of lowercase English letters

---

## 🧪 Sample Test Cases

### Input 1:

```
horse ros
```

### Output 1:

```
3
```

### Input 2:

```
intention execution
```

### Output 2:

```
5
```

---

## 💡 Explanation

* **Example 1:**

  * `horse` → `rorse` (replace 'h' with 'r')
  * `rorse` → `rose` (delete 'r')
  * `rose` → `ros` (delete 'e')
  * ✅ Total operations = **3**

* **Example 2:**

  * `intention` → `inention` (delete 't')
  * `inention` → `enention` (replace 'i' with 'e')
  * `enention` → `exention` (replace 'n' with 'x')
  * `exention` → `exection` (replace 'n' with 'c')
  * `exection` → `execution` (insert 'u')
  * ✅ Total operations = **5**

---

## ✅ Java Code – Top-Down Approach (Memoization)

```java
import java.util.*;

class EditDistanceMemo {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String a = sc.next();
        String b = sc.next();

        int m = a.length(), n = b.length();
        int[][] memo = new int[m + 1][n + 1];

        // Fill memo with -1 (unvisited)
        for (int[] row : memo) {
            Arrays.fill(row, -1);
        }

        System.out.println(editDistance(a, b, m, n, memo));
    }

    private static int editDistance(String a, String b, int m, int n, int[][] memo) {
        if (m == 0) return memo[m][n] = n;  // insert all of b
        if (n == 0) return memo[m][n] = m;  // delete all of a

        if (memo[m][n] != -1) return memo[m][n];

        if (a.charAt(m - 1) == b.charAt(n - 1)) {
            return memo[m][n] = editDistance(a, b, m - 1, n - 1, memo);
        }

        int insert = editDistance(a, b, m, n - 1, memo);
        int delete = editDistance(a, b, m - 1, n, memo);
        int replace = editDistance(a, b, m - 1, n - 1, memo);

        return memo[m][n] = 1 + Math.min(replace, Math.min(insert, delete));
    }
}
```

---

## ✅ Java Code – Bottom-Up Approach (Tabulation)

```java
import java.util.*;

class EditDistanceDP {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String a = sc.next();
        String b = sc.next();

        int m = a.length(), n = b.length();
        int[][] dp = new int[m + 1][n + 1];

        // Base case: converting from empty string
        for (int i = 0; i <= m; i++) dp[i][0] = i;
        for (int j = 0; j <= n; j++) dp[0][j] = j;

        // Build the table
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (a.charAt(i - 1) == b.charAt(j - 1)) {
                    dp[i][j] = dp[i - 1][j - 1]; // characters match
                } else {
                    dp[i][j] = 1 + Math.min(
                        dp[i - 1][j - 1],           // replace
                        Math.min(dp[i - 1][j],      // delete
                                 dp[i][j - 1])      // insert
                    );
                }
            }
        }

        System.out.println(dp[m][n]);
    }
}
```

---

## ⏱ Time & Space Complexity

| Approach        | Time Complexity | Space Complexity |
| --------------- | --------------- | ---------------- |
| Top-Down (Memo) | O(m × n)        | O(m × n)         |
| Bottom-Up (DP)  | O(m × n)        | O(m × n)         |

Where `m = word1.length()` and `n = word2.length()`

---

✅ Both solutions are efficient and correct under the given constraints (`word length ≤ 500`). The bottom-up version avoids recursion stack issues, while the top-down version is often simpler to understand.
