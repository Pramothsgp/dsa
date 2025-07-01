## Problem Statement

You are given a string `s` consisting of lowercase English letters. A duplicate removal consists of choosing two adjacent and equal letters and removing them.

We repeatedly make duplicate removals on `s` until we can no longer.

Return the final string after all such duplicate removals have been made. It can be proven that the answer is unique.

---

### Example 1

**Input:**  
`s = "abbaca"`

**Output:**  
`"ca"`

**Explanation:**  
For example, in `"abbaca"` we could remove `"bb"` since the letters are adjacent and equal, and this is the only possible move. The result of this move is that the string is `"aaca"`, of which only `"aa"` is possible, so the final string is `"ca"`.

---

### Example 2

**Input:**  
`s = "azxxzy"`

**Output:**  
`"ay"`

---

### Input format

The first line contains a single string `s` consisting of lowercase English letters.

### Output format

The output prints a single line containing the final string after all adjacent duplicate removals have been performed.

Refer to the sample output for formatting specifications.

---

### Code constraints

- `1 <= s.length <= 10^5`
- `s` consists of lowercase English letters.

---

### Sample test cases

**Input 1:**  
```
aabbaca
ca
```
**Output 1:**  
```
aca
```

**Input 2:**  
```
azxxzyz
xy
```
**Output 2:**  
```
ayz
```

---

```java
import java.util.*;

class RemoveDuplicates {
    public static void main(String[] args) {
        // Read input string from standard input
        String s = new Scanner(System.in).nextLine();
        // Print the result after removing duplicates
        System.out.println(removeDuplicate(s));
    }
    
    // Recursive function to remove adjacent duplicates
    private static String removeDuplicate(String s) {
        StringBuilder sb = new StringBuilder();
        for (int i = 0; i < s.length(); ) {
            char cur = s.charAt(i);
            int j = i + 1;
            // Find the next character that is different
            while (j < s.length() && cur == s.charAt(j)) {
                j++;
            }
            // If no duplicate, append the character
            if (j == i + 1) {
                sb.append(cur);
            }
            // Move to the next group of characters
            i = j;
        }
        // If no changes, return the string; else, recurse
        return sb.length() == s.length() ? s : removeDuplicate(sb.toString());
    }
}
```