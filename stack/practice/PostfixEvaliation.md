# Reverse Polish Notation (RPN) Evaluation

You're given a list of string tokens representing a mathematical expression written in **Reverse Polish Notation (RPN)**.

---

## 📚 What is Reverse Polish Notation?

- **Operators come after their operands.**
- For example: - `2 4 +` &rarr; **6** - `18 4 - 7 /` &rarr; **((18 - 4) / 7) = 2**

---

## 📝 Evaluation Rules

- Evaluate the expression **from left to right**.
- Each operator works on the **two most recent operands**.
- Supported operators: `+`, `-`, `*`, `/`
- **Division** is integer division, rounding towards zero (e.g., `3 / 2 = 1`, `-3 / 2 = -1`).

> **Assumptions:**
>
> - Input is always a valid RPN expression.
> - The result is always a valid integer.
> - The original input list should not be modified.

---

## 🔢 Input Format

- A single line containing **space-separated tokens** (numbers or operators).
- Each token is either: - A valid (possibly negative) integer, or - One of: `"+"`, `"-"`, `"*"`, `"/"`

---

## 🖨️ Output Format

- Print a **single integer** — the result of evaluating the RPN expression.

---

## ⛓️ Constraints

- `1 ≤ tokens.length ≤ 10⁴`
- Each `tokens[i]` is either: - An integer in the range `[-2³¹, 2³¹ − 1]`, or - One of: `"+"`, `"-"`, `"*"`, `"/"`

---

## 🧪 Sample Test Cases

### Input 1

```
5 1 2 + 4 * + 3 -
```

**Output 1**

```
14
```

---

### Input 2

```
10 6 9 3 + -11 * / * 17 + 5 +
```

**Output 2**

```
22
```

---

## 💻 Sample Java Implementation
```java
import java.util.*;

// Class to evaluate a postfix (RPN) expression
class PostfixEvaluation {
        public static void main(String[] args) {
                Scanner sc = new Scanner(System.in);
                try {
                        // Read input, split by whitespace, and evaluate
                        System.out.println(evaluate(sc.nextLine().trim().split("\\s+")));
                } catch (RuntimeException e) {
                        return;
                }
        }

        // Evaluates the RPN expression represented as a string array
        private static int evaluate(String[] s) {
                Stack<Integer> values = new Stack<>();
                for (String c : s) {
                        if (isOperator(c)) {
                                // Pop two operands and apply the operator
                                values.push(eval(values.pop(), values.pop(), c));
                        } else {
                                // Push operand to stack
                                values.push(Integer.parseInt(c));
                        }
                }
                // The result is on top of the stack
                return values.peek();
        }

        // Checks if the string is an operator
        private static boolean isOperator(String c) {
                return "+-/*".indexOf(c) != -1;
        }

        // Evaluates a single operation with two operands
        private static int eval(int b, int a, String c) {
                switch (c) {
                        case "+":
                                return a + b;
                        case "-":
                                return a - b;
                        case "*":
                                return a * b;
                        case "/":
                                if (b == 0) {
                                        throw new RuntimeException("Cannot divide by zero");
                                }
                                return a / b;
                        default:
                                return 0;
                }
        }
}
```
