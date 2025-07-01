# Length of Last Word

Given a string `s` consisting of words and spaces, return the length of the last word in the string.  
A word is a maximal substring consisting of non-space characters only.

---

## Example 1

**Input:**  
`s = "Hello World"`

**Output:**  
`5`

**Explanation:**  
The last word is `"World"` with length 5.

---

## Example 2

**Input:**  
`s = "   fly me   to   the moon  "`

**Output:**  
`4`

**Explanation:**  
The last word is `"moon"` with length 4.

---

## Example 3

**Input:**  
`s = "luffy is still joyboy"`

**Output:**  
`6`

**Explanation:**  
The last word is `"joyboy"` with length 6.

---

## Input format

The input consists of a single line string `s`, consisting of uppercase and lowercase English letters and possibly containing spaces.

- The string will not be empty and will contain at least one non-space character.

## Output format

The output consists of a single integer, representing the length of the last word in the string.

- A word is defined as a maximal substring consisting of non-space characters only.

Refer to the sample output for formatting specifications.

---

## Code constraints

- `1 <= s.length <= 10^4`
- `s` consists of only English letters and spaces `' '`.
- There will be at least one word in `s`.

---

## Sample test cases

**Input 1:**  
```
Hello World
```
**Output 1:**  
```
5
```

**Input 2:**  
```
    fly me   to   the moon  
```
**Output 2:**  
```
4
```

**Input 3:**  
```
luffy is still joyboy
```
**Output 3:**  
```
6
```

---

## Solution

```java
import java.util.*;

// Class to find the length of the last word in a string
class WordLength {
     public static void main(String[] args) {
          // Read the input string, trim leading/trailing spaces, and split by spaces
          String[] s = new Scanner(System.in).nextLine().trim().split(" ");
          // Print the length of the last word
          System.out.println(s[s.length - 1].length());
     }
}
```