## Problem Statement

Given two strings `s` and `t` of lengths `m` and `n` respectively, return the minimum window substring of `s` such that every character in `t` (including duplicates) is included in the window. If there is no such substring, return the empty string `""`.

### Example 1

**Input:**  
```
s = "ADOBECODEBANC"  
t = "ABC"
```
**Output:**  
```
"BANC"
```
**Explanation:**  
The minimum window substring "BANC" includes 'A', 'B', and 'C' from string t.

### Example 2

**Input:**  
```
s = "a"  
t = "a"
```

**Output:**  
```
"a"
```
**Explanation:**  
The entire string s is the minimum window.

### Example 3

**Input:**  
```
s = "a"  
t = "aa"
```
**Output:**  
```
""
```

**Explanation:**  
Both 'a's from t must be included in the window. Since the largest window of s only has one 'a', return empty string.

---

### Input format

- The first line contains a string `s`, representing the source text.
- The second line contains a string `t`, representing the set of characters to be included in the window.

### Output format

- The output prints a string representing the minimum window substring of `s` that contains all characters from `t` (including duplicates). If no such window exists, print an empty string.

Refer to the sample input and output for formatting specifications.

---

### Code constraints

- `m == s.length`
- `n == t.length`
- `1 ≤ m, n ≤ 50`
- `s` and `t` consist of uppercase and lowercase English letters.

---

---

```java
import java.util.*;

class MinimumWindowSubString {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String s = sc.nextLine();
        String t = sc.nextLine();
        System.out.println(minSubString(s, t));
    }

    // Returns the minimum window substring of s containing all characters of t
    private static String minSubString(String s, String t) {
        int n = t.length();
        int m = s.length();
        int[] count = new int[128]; // Frequency of characters in t
        for (char c : t.toCharArray()) {
            ++count[c];
        }
        int[] window = new int[128]; // Frequency of characters in current window
        int start = 0, left = 0, cnt = 0, res = Integer.MAX_VALUE;

        for (int right = 0; right < m; right++) {
            char ch = s.charAt(right);
            window[ch]++;
            // If character ch is needed and its count in window does not exceed its count in t
            if (window[ch] > 0 && window[ch] <= count[ch]) {
                cnt++;
            }

            // When all characters from t are included in the window
            if (cnt == n) {
                char c = s.charAt(left);
                // Shrink the window from the left if possible
                while (count[c] == 0 || window[c] > count[c]) {
                    window[c]--;
                    c = s.charAt(++left);
                }

                // Update result if current window is smaller
                if (res > right - left + 1) {
                    res = right - left + 1;
                    start = left;
                }
            }
        }
        // Return the minimum window substring, or empty string if not found
        return res == Integer.MAX_VALUE ? "" : s.substring(start, start + res);
    }
}
```