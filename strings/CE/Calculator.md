# Basic Calculator

Given a string `s` representing a valid expression, implement a basic calculator to evaluate it, and return the result of the evaluation.

> **Note:** You are not allowed to use any built-in function that evaluates strings as mathematical expressions, such as `eval()`.

## Example 1

**Input:**  
`s = "1 + 1"`

**Output:**  
`2`

## Example 2

**Input:**  
`s = " 2-1 + 2 "`

**Output:**  
`3`

## Example 3

**Input:**  
`s = "(1+(4+5+2)-3)+(6+8)"`

**Output:**  
`23`

---

### Input format

The input consists of a single line string `s` representing a valid mathematical expression (e.g., `"1 + (2 - 3)"`).

### Output format

The output prints a single integer — the evaluated mathematical expression result.

Refer to the sample output for the formatting specifications.

---

### Code constraints

The given test cases fall under the following constraints:

- `1 ≤ s.length ≤ 3 * 10^5`
- `s` consists of digits, `'+'`, `'-'`, `'('`, `')'`, and `' '`.
- `s` represents a valid expression.
- `'+'` is not used as a unary operation (i.e., `"+1"` and `"+(2 + 3)"` are invalid).
- `'-'` could be used as a unary operation (i.e., `"-1"` and `"-(2 + 3)"` are valid).
- There will be no two consecutive operators in the input.
- Every number and running calculation will fit in a signed 32-bit integer.

---

### Sample test cases

**Input 1:**  
```
1 + 1
```
**Output 1:**  
```
2
```

**Input 2:**  
```
2-1 + 2 
```
**Output 2:**  
```
3
```

**Input 3:**  
```
(1+(4+5+2)-3)+(6+8)
```
**Output 3:**  
```
23
```

---
## For + & -

```java
import java.util.*;

class EvaluateString {
    static int i; // Index to track current position in the string

    public static void main(String[] args) {
        String s = new Scanner(System.in).nextLine();
        try {
            i = 0;
            System.out.println(evaluate(s));
        } catch (ArithmeticException | EmptyStackException e) {
            System.out.println("Invalid input");
        }
    }

    // Evaluates the expression containing only + and - (with parentheses)
    private static int evaluate(String s) {
        int num = 0, ans = 0;
        int sign = 1; // 1 for '+', -1 for '-'

        while (i < s.length()) {
            char c = s.charAt(i++);

            if (Character.isDigit(c)) {
                // Build the current number
                num = num * 10 + (c - '0');
            } else if (c == '(') {
                // Start a new evaluation for the sub-expression
                num = evaluate(s);
            } else if (c == ')') {
                // End of current sub-expression, return result
                return ans + num * sign;
            } else if (c == '+' || c == '-') {
                // Apply the previous sign and number to the result
                ans += num * sign;
                num = 0;
                sign = c == '-' ? -1 : 1; // Update sign for next number
            }
            // Ignore spaces and other characters as per constraints
        }

        // Add any remaining number to the result
        return ans + num * sign;
    }
}
```

## For *, /, +, -

```java
import java.util.*;

class EvaluateString {
    public static void main(String[] args) {
        // Read the input expression from standard input
        String s = new Scanner(System.in).nextLine();
        try {
            // Evaluate the expression and print the result
            System.out.println(evaluate(s));
        } catch (ArithmeticException | EmptyStackException e) {
            // Handle invalid input or arithmetic errors
            System.out.println("Invalid input");
        }
    }
    
    // Evaluates the mathematical expression represented by string s
    private static int evaluate(String s) {
        Stack<Integer> values = new Stack<>();      // Stack to store integer values
        Stack<Character> operations = new Stack<>(); // Stack to store operators
        
        for (int i = 0; i < s.length(); i++) {
            char c = s.charAt(i);
            if (c == ' ') continue; // Skip spaces
            
            // If the character is a digit, parse the full number
            if (Character.isDigit(c)) {
                int num = 0;
                while (i < s.length() && Character.isDigit(s.charAt(i))) {
                    num = num * 10 + s.charAt(i++) - '0';
                }
                i--;
                values.push(num);
            } else if (c == '(') {
                // Push '(' to operations stack
                operations.push(c);
            } else if (c == ')') {
                // Evaluate the expression inside the parentheses
                while (operations.peek() != '(') {
                    values.push(eval(values.pop(), values.pop(), operations.pop()));
                }
                operations.pop(); // Remove '(' from stack
            } else if (isOperator(c)) {
                // Evaluate operators with higher or equal precedence
                while (!operations.isEmpty() && precedence(c) <= precedence(operations.peek())) {
                    values.push(eval(values.pop(), values.pop(), operations.pop()));
                }
                operations.push(c);
            }
        }
        
        // Evaluate any remaining operations
        while (!operations.isEmpty()) {
            values.push(eval(values.pop(), values.pop(), operations.pop()));
        }
        
        // The result is on top of the values stack
        return values.peek();
    }
    
    // Returns the precedence of the operator
    private static int precedence(char c) {
        switch (c) {
            case '*':
            case '/':
                return 2;
            case '+':
            case '-':
                return 1;
            default:
                return -1;
        }
    }
    
    // Checks if the character is a valid operator
    private static boolean isOperator(char c) {
        return "+-*/".indexOf(c) != -1;
    }
    
    // Evaluates a simple expression with two operands and an operator
    private static int eval(int b, int a, char op) {
        switch (op) {
            case '+':
                return a + b;
            case '-':
                return a - b;
            case '*':
                return a * b;
            case '/':
                return a / b;
            default:
                return 0;
        }
    }
}
```