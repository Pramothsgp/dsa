# Reverse Words in a String

Given an input string `s`, reverse the order of the words.

A word is defined as a sequence of non-space characters. The words in `s` will be separated by at least one space.

Return a string of the words in reverse order, concatenated by a single space.

> **Note:**  
> - `s` may contain leading or trailing spaces or multiple spaces between two words.  
> - The returned string should only have a single space separating the words.  
> - Do not include any extra spaces.

---

## Examples

**Example 1:**

```
Input:  s = the sky is blue
Output: blue is sky the
```

**Example 2:**

```
Input:  s =   hello world  
Output: world hello
Explanation: Your reversed string should not contain leading or trailing spaces.
```

**Example 3:**

```
Input:  s = a good   example
Output: example good a
Explanation: You need to reduce multiple spaces between two words to a single space in the reversed string.
```

---

## Input format

The input is a single string `s` containing words separated by spaces.

## Output format

The output is a string containing the words in reverse order, with exactly one space between each word.

Refer to the sample output for formatting specifications.

---

## Code constraints

- `1 ≤ s.length ≤ 10^4`
- `s` contains English letters (upper-case and lower-case), digits, and spaces `' '`.
- There is at least one word in `s`.

---

## Sample test cases

```
Input 1 :
the sky is blue
Output 1 :
blue is sky the

Input 2 :
hello world  
Output 2 :
world hello

Input 3 :
a good example
Output 3 :
example good a
```

---

## Java Implementation

```java
import java.util.*;

class ReverseString {
    public static void main(String[] args) {
        // Read the input string, trim leading/trailing spaces, and split by spaces
        String[] s = new Scanner(System.in).nextLine().trim().split(" ");
        // Iterate over the words array in reverse order and print each word
        for (int i = s.length - 1; i >= 0; i--) {
            System.out.printf("%s ", s[i]);
        }
    }
}
```