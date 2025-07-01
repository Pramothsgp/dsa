# Word Pattern

Given a pattern and a string `s`, determine if `s` follows the same pattern.

**Here, "follow" means a full match, such that there is a bijection between a letter in the pattern and a non-empty word in `s`. Specifically:**

- Each letter in the pattern maps to exactly one unique word in `s`.
- Each unique word in `s` maps to exactly one letter in the pattern.
- No two letters map to the same word, and no two words map to the same letter.

---

## Examples

**Example 1:**

```
Input: pattern = "abba", s = "dog cat cat dog"
Output: true

Explanation:
The bijection can be established as:
'a' maps to "dog".
'b' maps to "cat".
```

**Example 2:**

```
Input: pattern = "abba", s = "dog cat cat fish"
Output: false
```

**Example 3:**

```
Input: pattern = "aaaa", s = "dog cat cat dog"
Output: false
```

---

## Input format

- The first line contains the pattern string.
- The second line contains the string `s`.

## Output format

- Print `true` if `s` follows the same pattern, `false` otherwise.

Refer to the sample output for formatting specifications.

---

## Code constraints

- `1 <= pattern.length <= 300`
- The pattern contains only lower-case English letters.
- `1 <= s.length <= 3000`
- `s` contains only lowercase English letters and spaces `' '`.
- `s` does not contain any leading or trailing spaces.
- All the words in `s` are separated by a single space.

---

## Sample test cases

**Input 1:**
```
abba
dog cat cat dog
```
**Output 1:**
```
true
```

**Input 2:**
```
abba
dog cat cat fish
```
**Output 2:**
```
false
```

**Input 3:**
```
aaaa
dog cat cat dog
```
**Output 3:**
```
false
```

---

## Java Implementation

```java
import java.util.*;

class WordPattern {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        // Read the pattern string
        String pattern = sc.nextLine().trim();
        // Read the input string and split into words
        String[] words = sc.nextLine().trim().split(" ");
        // Print the result of the pattern match
        System.out.println(match(pattern, words));
    }
    
    // Function to check if the pattern matches the words
    private static boolean match(String pattern, String[] words) {
        // If lengths do not match, return false
        if (pattern.length() != words.length) return false;
        // Map to store character to word mapping
        Map<Character, String> patternMap = new HashMap<>();
        // Map to store word to character mapping
        Map<String, Character> wordMap = new HashMap<>();
        for (int i = 0; i < words.length; i++) {
            // If the character is already mapped
            if (patternMap.containsKey(pattern.charAt(i))) {
                // Check if it maps to the same word
                if (!patternMap.get(pattern.charAt(i)).equals(words[i])) {
                    return false;
                }
            // If the word is already mapped
            } else if (wordMap.containsKey(words[i])) {
                // Check if it maps to the same character
                if (wordMap.get(words[i]) != pattern.charAt(i)) {
                    return false;
                }
            } else {
                // Create new mappings
                wordMap.put(words[i], pattern.charAt(i));
                patternMap.put(pattern.charAt(i), words[i]);
            }
        }
        return true;
    }
}
```