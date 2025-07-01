# Longest Common Prefix

Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string `""`.

---

## Example 1

**Input**
```
3
flower
flow
flight
```
**Output**
```
"fl"
```
**Explanation:**  
All three words start with "fl", so that is the longest common prefix.  
After "fl", the third word "flight" differs from "flow" and "flower".  
Hence, "fl" is the longest common starting sequence in all strings.

---

## Example 2

**Input**
```
3
dog
racecar
car
```
**Output**
```
""
```
**Explanation:**  
There is no common prefix among the input strings.

---

### Input format

- The first line contains an integer `n` — the number of strings.
- The next `n` lines each contain a string (lowercase English letters only).

### Output format

- The output consists of a single line containing the longest common prefix among all the input strings.
- If there is no common prefix, output an empty string (i.e., just print nothing).

Refer to the sample output for formatting specifications.

---

### Code constraints

- `1 <= strs.length <= 200`
- `0 <= strs[i].length <= 200`
- `strs[i]` consists of only lowercase English letters if it is non-empty.

---

### Sample test cases

**Input 1:**
```
3
flower
flow
flight
```
**Output 1:**
```
"fl"
```

**Input 2:**
```
3
dog
racecar
car
```
**Output 2:**
```
""
```

---

```java
import java.util.*;

class CommonPrefix {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        String[] s = new String[n];
        // Read n strings from input
        for (int i = 0; i < n; i++) {
            s[i] = sc.next();
        }
        // Print the longest common prefix
        System.out.println(findCommonPrefix(s));
    }

    // Function to find the longest common prefix among all strings
    private static String findCommonPrefix(String[] s) {
        int n = s.length;
        // Find the shortest string in the array
        String minStr = s[0];
        for (String w : s) {
            if (w.length() < minStr.length()) {
                minStr = w;
            }
        }
        String res = "";
        // Check each prefix of the shortest string
        for (int i = 1; i <= minStr.length(); i++) {
            String substr = minStr.substring(0, i);
            boolean flag = true;
            // Verify if all strings start with the current prefix
            for (String w : s) {
                if (!w.startsWith(substr)) {
                    flag = false;
                    break;
                }
            }
            if (!flag) break;
            res = substr;
        }
        // Return the result wrapped in quotes
        return "\"" + res + "\"";
    }
}
```