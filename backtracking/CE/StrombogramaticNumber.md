# 🔄 Strobogrammatic Numbers Generator

A **strobogrammatic number** is one that appears the same when rotated 180°. For example:

```
69 → 180° → 96 ✅
88 → 180° → 88 ✅
962 → 180° → 296 ❌
```

---

## 📌 Problem Statement

> Given an integer `n`, return **all strobogrammatic numbers** of length `n`.

---

## 🧾 Input Format

* A single integer `n` (1 ≤ n ≤ 8)

## 🖨 Output Format

* Print all valid strobogrammatic numbers of length `n`, **space-separated**

---

## 🧪 Sample Inputs and Outputs

| Input | Output        |
| ----- | ------------- |
| `1`   | `0 1 8`       |
| `2`   | `11 88 69 96` |

---

## ✅ Valid Digit Mappings (180° Rotation)

| Original | Rotated |
| -------- | ------- |
| `0`      | `0`     |
| `1`      | `1`     |
| `6`      | `9`     |
| `8`      | `8`     |
| `9`      | `6`     |

---

## 💡 Approach

We use **recursive backtracking**:

1. Build numbers from **inside → out**, adding **valid digit pairs** to both sides.
2. Stop when the desired length is built.
3. Avoid leading zeros unless `n == total`.

---

## 👨‍💻 Java Code (Well-Formatted with Comments)

```java
import java.util.*;

class StroboGrammer {

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();  // Read the desired length
        List<String> result = build(n, n);

        // Print all results space-separated
        System.out.println(String.join(" ", result));
    }

    /**
     * Recursively builds strobogrammatic numbers of length 'n'
     * @param n     - Current level of recursion (remaining characters)
     * @param total - Original length to prevent adding leading zero
     * @return      - List of valid strobogrammatic numbers
     */
    private static List<String> build(int n, int total) {
        // Base case 1: empty string for even length
        if (n == 0) return Arrays.asList("");

        // Base case 2: middle characters for odd length
        if (n == 1) return Arrays.asList("0", "1", "8");

        // Recursive step: get subresults of length n - 2
        List<String> subList = build(n - 2, total);
        List<String> res = new ArrayList<>();

        for (String s : subList) {
            // Only add "0...0" if it's not the outermost layer
            if (n != total) res.add("0" + s + "0");

            res.add("1" + s + "1");
            res.add("8" + s + "8");
            res.add("6" + s + "9");
            res.add("9" + s + "6");
        }

        return res;
    }
}
```

---

## 🧠 Time & Space Complexity

| Metric | Value                                    |
| ------ | ---------------------------------------- |
| Time   | `O(5^(n/2))` (recursively tries 5 pairs) |
| Space  | `O(5^(n/2))` (result storage)            |

---

## ✅ Test This With

```
Input:
3

Output:
101 609 808 906 111 619 818 916 181 689 888 986
```

(⚠ Note: Outputs may vary in order)

---