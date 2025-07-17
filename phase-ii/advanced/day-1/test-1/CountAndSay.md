
# 🗣️ Count and Say – Single File Java Program



## 📝 Problem Statement

The **"count-and-say"** sequence is a sequence of digit strings defined as:

- `countAndSay(1) = "1"`
- `countAndSay(n)` is the **run-length encoding (RLE)** of `countAndSay(n - 1)`

### ℹ️ What is Run-Length Encoding?

Run-length encoding is a form of compression where **consecutive identical digits** are encoded as:



<count><digit>

For example:
- `"1"` → one 1 → `"11"`
- `"11"` → two 1s → `"21"`
- `"21"` → one 2, one 1 → `"1211"`

---

## 📥 Input Format

- A single integer `n` (1 ≤ n ≤ 30)

## 📤 Output Format

- A string representing the **nth** term of the **Count and Say** sequence

---

## 🧪 Sample Test Cases

### Input 1:
```

1

```

### Output 1:
```

1

```

---

### Input 2:
```

4

```

### Output 2:
```

1211

````

---

## 🧠 Explanation

- countAndSay(1) = "1"
- countAndSay(2) = RLE("1") → "11"
- countAndSay(3) = RLE("11") → "21"
- countAndSay(4) = RLE("21") → "1211"

---

## 💻 Java Code

```java
import java.util.*;

/**
 * 🔢 Count and Say Sequence Generator
 * 
 * Generates the nth term in the Count and Say sequence using run-length encoding.
 */
public class Strings {
    public static void main(String[] args) {
        // 📥 Read input
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();

        // 🧾 Initialize the first element of the sequence
        String result = "1";

        // 🔄 Iteratively build up to the nth term
        while (--n > 0) {
            result = countAndSay(result);
        }

        // 📤 Print the result
        System.out.println(result);
    }

    /**
     * 🧮 countAndSay:
     * Applies run-length encoding to the given string.
     * For example: "3322251" → "23321511"
     */
    private static String countAndSay(String s) {
        StringBuilder sb = new StringBuilder();
        int count = 1;

        // 🔁 Traverse the string
        for (int i = 1; i < s.length(); i++) {
            if (s.charAt(i) == s.charAt(i - 1)) {
                count++; // same char, increase count
            } else {
                // append count and previous char
                sb.append(count).append(s.charAt(i - 1));
                count = 1; // reset count
            }
        }

        // ⏹️ Append the last run
        sb.append(count).append(s.charAt(s.length() - 1));

        return sb.toString();
    }
}
````

---

## 🧠 Time and Space Complexity

* **Time Complexity:** O(n \* m), where `m` is the average length of the sequence string at each step
* **Space Complexity:** O(m) — for building the next term

---

## ✅ Notes

* This solution uses **iterative RLE** to generate terms from 1 to `n`.
* Each string is processed and transformed one-by-one.
* Efficient for `n ≤ 30` as per constraints.

---

Happy coding! 🚀
