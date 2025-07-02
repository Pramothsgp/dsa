# Problem Statement

Write a function that determines whether a given string contains balanced brackets. The string may contain other characters, but only the brackets `()`, `[]`, and `{}` influence whether it is balanced.

A string is balanced if:

- Every opening bracket has a corresponding and correctly ordered closing bracket.
- Brackets are closed in the correct order (e.g., `[(])` is not allowed).
- Brackets of different types do not improperly overlap.

## Input format

A single line string `s` containing any printable characters, including:

- Brackets: `()`, `[]`, `{}`
- Other characters (letters, digits, symbols, spaces, etc.)

## Output format

Print `true` if the brackets in the string are balanced, else print `false`.

## Code constraints

- `1 ≤ s.length ≤ 10^5`
- The string may contain any characters, but only brackets should be used to determine balance.

## Sample test cases

**Input 1:**
```
([])(){}(())()()
```
**Output 1:**
```
true
```

**Input 2:**
```
()[]{}{
```
**Output 2:**
```
false
```

---
## Java Solution

```java
import java.util.*;

class ParanthesisChecker{
    public static void main(String[] args){
        // Read input string from standard input
        String s = new Scanner(System.in).nextLine();
        // Print the result of the bracket balance check
        System.out.println(checkParanthesis(s));
    }
    
    // Function to check if the brackets in the string are balanced
    private static boolean checkParanthesis(String s){
        Stack<Character> stack = new Stack<>();
        for(char c : s.toCharArray()){
            // If stack is empty, push the current character
            if(stack.isEmpty()){
                stack.push(c);
            } 
            // If the top of the stack and current character form a matching pair, pop the stack
            else if(stack.peek() == '[' && c == ']' || stack.peek() == '{' && c == '}' || stack.peek() == '(' && c == ')'){
                stack.pop();
            } 
            // Otherwise, push the current character onto the stack
            else{
                stack.push(c);
            }
        }
        // If stack is empty, all brackets are balanced
        return stack.isEmpty();
    }
}
```