# Interleaving String

Given strings `s1`, `s2`, and `s3`, find whether `s3` is formed by an interleaving of `s1` and `s2`.

An **interleaving** of two strings `s` and `t` is a configuration where `s` and `t` are divided into `n` and `m` substrings, respectively, such that:

- `s = s1 + s2 + ... + sn`
- `t = t1 + t2 + ... + tm`
- `|n - m| <= 1`
- The interleaving is `s1 + t1 + s2 + t2 + s3 + t3 + ...` or `t1 + s1 + t2 + s2 + t3 + s3 + ...`

> **Note:** `a + b` is the concatenation of strings `a` and `b`.

![Interleaving Example](https://assets.leetcode.com/uploads/2020/09/02/interleave.jpg)

---

## Examples

### Example 1

**Input:**
```
s1 = "aabcc"
s2 = "dbbca"
s3 = "aadbbcbcac"
```
**Output:** `true`

**Explanation:**  
One way to obtain `s3` is:  
Split `s1` into `"aa" + "bc" + "c"`, and `s2` into `"dbbc" + "a"`.  
Interleaving the two splits, we get `"aa" + "dbbc" + "bc" + "a" + "c" = "aadbbcbcac"`.  
Since `s3` can be obtained by interleaving `s1` and `s2`, we return `true`.

---

### Example 2

**Input:**
```
s1 = "aabcc"
s2 = "dbbca"
s3 = "aadbbbaccc"
```
**Output:** `false`

**Explanation:**  
It is impossible to interleave `s2` with any other string to obtain `s3`.

---

### Example 3

**Input:**
```
s1 = ""
s2 = ""
s3 = ""
```
**Output:** `true`

---

## Input format

- The first line contains the string `s1`.
- The second line contains the string `s2`.
- The third line contains the string `s3`.

## Output format

- Print `"true"` if an interleaving of `s1` and `s2` forms `s3`.
- Otherwise, print `"false"`.

Refer to the sample output for formatting specifications.

---

## Code constraints

- `0 <= s1.length, s2.length <= 100`
- `0 <= s3.length <= 200`
- `s1`, `s2`, and `s3` consist of lowercase English letters.

---

## Sample test cases

**Input 1:**
```
aabcc
dbbca
aadbbcbcac
```
**Output 1:**
```
true
```

**Input 2:**
```
aabcc
dbbca
aadbbbaccc
```
**Output 2:**
```
false
```

---

## Java Implementation

```java
import java.util.*;

class InterLeavingString {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String a = sc.nextLine();
        String b = sc.nextLine();
        String c = sc.nextLine();
        // Call the recursive function to check interleaving
        System.out.println(isInterLeavingString(a, b, c, 0, 0, 0));
    }

    // Recursive function to check if c can be formed by interleaving a and b
    private static boolean isInterLeavingString(String a, String b, String c, int i, int j, int k) {
        int n = a.length();
        int m = b.length();
        // If all characters from a and b are used and k reaches end of c
        if (i + j == c.length()) return true;
        // If both a[i] and b[j] match c[k], try both possibilities
        if (i < n && j < m && a.charAt(i) == c.charAt(k) && b.charAt(j) == c.charAt(k)) {
            return isInterLeavingString(a, b, c, i + 1, j, k + 1) || isInterLeavingString(a, b, c, i, j + 1, k + 1);
        }
        // If a[i] matches c[k], move forward in a
        if (i < n && a.charAt(i) == c.charAt(k)) {
            return isInterLeavingString(a, b, c, i + 1, j, k + 1);
        }
        // If b[j] matches c[k], move forward in b
        if (j < m && b.charAt(j) == c.charAt(k)) {
            return isInterLeavingString(a, b, c, i, j + 1, k + 1);
        }
        // If no match, return false
        return false;
    }
}
```

---

## Algorithm with Memoization

To optimize the recursive approach and avoid recomputation, use memoization to store already computed states.

```java
import java.util.*;

class InterLeavingStringMemo {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String a = sc.nextLine();
        String b = sc.nextLine();
        String c = sc.nextLine();
        // Create a memoization table
        Boolean[][] memo = new Boolean[a.length() + 1][b.length() + 1];
        System.out.println(isInterLeavingString(a, b, c, 0, 0, memo));
    }

    // Recursive function with memoization
    private static boolean isInterLeavingString(String a, String b, String c, int i, int j, Boolean[][] memo) {
        if (i + j == c.length()) return true;
        if (memo[i][j] != null) return memo[i][j];
        boolean ans = false;
        if (i < a.length() && a.charAt(i) == c.charAt(i + j)) {
            ans = ans || isInterLeavingString(a, b, c, i + 1, j, memo);
        }
        if (j < b.length() && b.charAt(j) == c.charAt(i + j)) {
            ans = ans || isInterLeavingString(a, b, c, i, j + 1, memo);
        }
        memo[i][j] = ans;
        return ans;
    }
}
```
