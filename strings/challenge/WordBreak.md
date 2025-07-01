# Word Break

Given a string `s` and a dictionary of strings `wordDict`, return `true` if `s` can be segmented into a space-separated sequence of one or more dictionary words.

> **Note:** The same word in the dictionary may be reused multiple times in the segmentation.

---

## Examples

### Example 1

```
Input:  s = leetcode
    wordDict = leet code
Output: true

Explanation: "leetcode" can be segmented as "leet code".
```

### Example 2

```
Input:  s = applepenapple
    wordDict = apple pen
Output: true

Explanation: "applepenapple" can be segmented as "apple pen apple".
Note that you are allowed to reuse a dictionary word.
```

### Example 3

```
Input:  s = catsandog
    wordDict = cats dog sand and cat
Output: false
```

---

## Input Format

- The first line contains a string `s`, representing the string to be segmented.
- The second line contains a space-separated list of words, representing the `wordDict`.

## Output Format

- Output a boolean value: `true` if `s` can be segmented into words from `wordDict`, otherwise `false`.

Refer to the sample output for formatting specifications.

---

## Constraints

- `1 ≤ s.length ≤ 300`
- `1 ≤ wordDict.length ≤ 1000`
- `1 ≤ wordDict[i].length ≤ 20`
- `s` and `wordDict[i]` consist of only lowercase English letters.
- All the strings of `wordDict` are unique.

---

## Sample Test Cases

```
Input 1:
leetcode
leet code
Output 1:
true

Input 2:
applepenapple
apple pen
Output 2:
true

Input 3:
catsandog
cats dog sand and cat
Output 3:
false
```

---

## Java Implementation

```java
import java.util.*;

class WordBreak {
    public static void main(String[] args) {
    Scanner sc = new Scanner(System.in);
    String s = sc.next(); // Read the string to be segmented
    List<String> dict = new ArrayList<>();
    // Read the dictionary words
    while (sc.hasNext()) {
        dict.add(sc.next());
    }
    System.out.println(wordBreak(s, dict)); // Output the result
    }

    // Function to determine if s can be segmented using words from l
    private static boolean wordBreak(String s, List<String> l) {
    int n = s.length();
    boolean[] dp = new boolean[n + 1]; // dp[i] is true if s[0..i-1] can be segmented
    dp[0] = true;
    int max_len = 0;
    // Find the maximum word length in the dictionary
    for (String str : l) {
        max_len = Math.max(max_len, str.length());
    }
    // Dynamic programming to check all possible segmentations
    for (int i = 1; i <= n; i++) {
        for (int j = i - 1; j >= Math.max(i - max_len - 1, 0); j--) {
        if (dp[j] && l.contains(s.substring(j, i))) {
            dp[i] = true;
            break;
        }
        }
    }
    return dp[n];
    }
}
```