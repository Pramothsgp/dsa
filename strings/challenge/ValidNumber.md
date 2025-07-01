# Valid Number

Given a string `s`, return whether `s` is a valid number.

## Valid Examples

All the following are valid numbers:

- `"2"`
- `"0089"`
- `"-0.1"`
- `"+3.14"`
- `"4."`
- `"- .9"`
- `"2e10"`
- `"-90E3"`
- `"3e+7"`
- `"+6e-1"`
- `"53.5e93"`
- `"-123.456e789"`

## Invalid Examples

The following are **not** valid numbers:

- `"abc"`
- `"1a"`
- `"1e"`
- `"e3"`
- `"99e2.5"`
- `"--6"`
- `"-+3"`
- `"95a54e53"`

## Formal Definition

A valid number is defined as:

- An integer number followed by an optional exponent.
- A decimal number followed by an optional exponent.

### Integer Number

An integer number is defined as an optional sign (`'-'` or `'+'`) followed by digits.

### Decimal Number

A decimal number is defined as an optional sign (`'-'` or `'+'`) followed by one of the following:

- Digits followed by a dot `'.'`
- Digits followed by a dot `'.'` and more digits
- A dot `'.'` followed by digits

### Exponent

An exponent is defined as an exponent notation (`'e'` or `'E'`) followed by an integer number.

### Digits

Digits are defined as one or more digits.

---

## Input Format

The input contains a single string `s`, representing the value to be validated as a number.

## Output Format

Print `"true"` if the string represents a valid number, otherwise print `"false"`.

Refer to the sample output for formatting.

## Code Constraints

- `1 ≤ s.length ≤ 20`
- `s` consists of only English letters (both uppercase and lowercase), digits (`0-9`), plus `'+'`, minus `'-'`, or dot `'.'`.

---

## Sample Test Cases

**Input 1:**
```
0
```
**Output 1:**
```
true
```

**Input 2:**
```
e
```
**Output 2:**
```
false
```

**Input 3:**
```
.
```
**Output 3:**
```
false
```

---

## Java Solution

```java
import java.util.*;

class ValidNumber {
    public static void main(String[] args) {
        try {
            Scanner sc = new Scanner(System.in);
            String s = sc.nextLine();
            System.out.println(isNumber(s));
        } catch (NoSuchElementException e) {
            // If no input is provided, print false
            System.out.println(false);
        }
    }
    
    // Function to check if the string is a valid number
    private static boolean isNumber(String s) {
        s = s.trim(); // Remove leading and trailing spaces
        // Regex to match valid numbers as per the definition
        String regex = "^[+-]?((\\d+\\.?\\d*)|(\\.\\d+))([eE][+-]?\\d+)?$";
        return s.matches(regex);
    }
}
```
