# Largest Number After Removing k Digits

Given a positive integer represented as a string and an integer `k`, remove exactly `k` digits to form the **largest possible number**, while maintaining the original relative order of the remaining digits.

---

## Input Format

- **First line:** A string `number` (no leading zeros unless the number is `"0"`).
- **Second line:** An integer `k` (number of digits to remove).

---

## Output Format

- Print a single string: the largest number possible after removing exactly `k` digits.
- If `k` is greater than or equal to the number of digits, print an error message.

---

## Constraints

- `0 ≤ k < number.length`
- `number` contains only digits `0–9`
- `number` does not start with `0` unless it is `"0"`

---

## Sample Test Cases

### Input 1
```
462839
10
```
**Output 1**
```
Error: Cannot remove more digits than the number has.
```

---

### Input 2
```
987638464
3
```
**Output 2**
```
988464
```

---
## Java Implementation

```java
import java.util.*;

class GreatestNumber {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        // Read input and print the result of findGreatestNumber
        System.out.println(findGreatestNumber(sc.nextLine(), sc.nextInt()));
    }
    
    // Function to find the largest number after removing k digits
    private static String findGreatestNumber(String s, int k) {
        // If k is greater than or equal to the length of the number, return error
        if (s.length() <= k) {
            return "Error: Cannot remove more digits than the number has.";
        }
        StringBuilder sb = new StringBuilder();
        // Iterate through each digit in the string
        for (char c : s.toCharArray()) {
            if (sb.length() == 0) {
                sb.append(c);
            } else {
                // Remove smaller digits from the end while k > 0 and current digit is larger
                while (k > 0 && sb.length() > 0 && sb.charAt(sb.length() - 1) < c) {
                    sb.deleteCharAt(sb.length() - 1);
                    k--;
                }
                sb.append(c);
            }
        }
        // If k digits are still left to remove, remove from the end
        while (k > 0 && sb.length() > 0) {
            sb.deleteCharAt(sb.length() - 1);
            k--;
        }
        // Return the resulting largest number as a string
        return sb.toString();
    }
}
```
