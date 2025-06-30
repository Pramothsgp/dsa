## Problem Statement

Given an integer `x`, return `true` if `x` is a palindrome, and `false` otherwise.

---

### Example 1

**Input:**  
`x = 121`  
**Output:**  
`true`  
**Explanation:**  
121 reads as 121 from left to right and from right to left.

---

### Example 2

**Input:**  
`x = -121`  
**Output:**  
`false`  
**Explanation:**  
From left to right, it reads -121. From right to left, it becomes 121-. Therefore, it is not a palindrome.

---

### Example 3

**Input:**  
`x = 10`  
**Output:**  
`false`  
**Explanation:**  
Reads 01 from right to left. Therefore, it is not a palindrome.

---

### Input format

The input consists of a single integer `x`.

---

### Output format

The output consists of a single line:

- `"true"` if `x` is a palindrome number.
- `"false"` if `x` is not a palindrome number.

Refer to the sample output for formatting specifications.

---

### Code constraints

- -2<sup>31</sup> ≤ x ≤ 2<sup>31</sup> - 1

---

### Sample test cases

**Input 1:**  
`-121`  
**Output 1:**  
`false`

**Input 2:**  
`121`  
**Output 2:**  
`true`

---

```java
import java.util.*;

class Palindrome{
    public static void main(String[] args){
        // Read integer input from user
        int n = new Scanner(System.in).nextInt();
        // Print whether the number is a palindrome
        System.out.println(isPal(n));
    }
    
    // Function to check if a number is a palindrome
    private static boolean isPal(int n){
        // Negative numbers are not palindromes
        if(n < 0) return false;
        int x = n , sum = 0;
        // Reverse the number
        while(x > 0){
            sum = sum * 10  + x % 10;
            x /= 10;
        }
        // Check if reversed number is equal to original
        return sum == n;
    }
}
```