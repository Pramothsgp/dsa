## Problem Statement

Sharon is fascinated by palindromes and wants to find the length of the longest palindromic substring in a given string.

Write a program for Sharon that takes a string as input and outputs the length of the longest palindromic substring.

---

### Example

**Input:**
```
bananas
```
**Output:** 
```
5
```
**Explanation:**  
The longest palindromic substring is `'anana'` with a length of 5.

---

### Input format

The input consists of a string.

### Output format

The output prints the integer, representing the length of the longest palindromic substring.

Refer to the sample output for formatting specifications.

---

### Code constraints

- The string contains lowercase letters with at most 50 characters.

---

### Sample test cases

**Input 1 :**
```
bananas
```
**Output 1 :**
```
5
```

**Input 2 :**
```
acacacab
```
**Output 2 :**
```
7
```

---

## Memoization

```java
import java.util.*;

// Recursive approach with memoization
class PalindromicSubString{
    public static void main(String[] args){
        String s = new Scanner(System.in).nextLine();
        int n = s.length();
        int[][] memo = new int[n][n];
        // Initialize memoization table with -1
        for(int[] row : memo){
            Arrays.fill(row , -1);
        }
        
        // Print the length of the longest palindromic substring
        System.out.println(lps(s , 0 , n - 1 , memo));
    }
    
    // Recursive function to find the longest palindromic substring
    private static int lps(String s , int left , int right , int[][] memo){
        if(left > right) return 0; // Base case: invalid substring
        if(left == right) return 1; // Base case: single character
        
        if(memo[left][right] != -1) return memo[left][right]; // Return if already computed
        
        if(s.charAt(left) == s.charAt(right)){
            // If characters match, include them and check the inner substring
            return memo[left][right] = lps(s , left + 1 , right - 1 , memo) + 2;
        }
        
        // Otherwise, take the maximum by excluding one character from either end
        return memo[left][right] = Math.max(lps(s , left + 1 , right , memo) , lps(s , left , right - 1 , memo));
    }
}
```

---
## Dynamic Programming

```java
import java.util.*;

// Dynamic programming approach
class PalindromicSubString{
    public static void main(String[] args){
        String s = new Scanner(System.in).nextLine();
        System.out.println(lps(s));
    }
    
    // Function to find the longest palindromic substring using DP
    private static int lps(String s){
        int n = s.length();
        int[][] dp = new int[n][n];
        // Fill the DP table
        for(int i=n-1;i>=0;i--){
            for(int j=i;j<n;j++){
                if(i == j){
                    dp[i][j] = 1; // Single character is a palindrome
                    continue;
                }
                if(s.charAt(i) == s.charAt(j)){
                    if(i + 1 == j){
                        dp[i][j] = 2; // Two matching characters
                    } else {
                        dp[i][j] = dp[i+1][j-1] + 2; // Expand around the center
                    }
                } else {
                    dp[i][j] = Math.max(dp[i  + 1][j] , dp[i][j - 1]); // Exclude one end
                }
            }
        }
        
        return dp[0][n - 1]; // Result for the whole string
    }
}
```