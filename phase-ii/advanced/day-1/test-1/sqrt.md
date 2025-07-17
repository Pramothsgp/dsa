
## 🔢 Square Root of a Number (⎷x)

---

### 📝 Problem Statement

Given a non-negative integer `x`, return **the square root of x**, rounded **down** to the nearest integer.

> ❌ You **must NOT** use built-in functions like `Math.sqrt`, `pow(x, 0.5)`, or `x ** 0.5`.

---

### 📥 Input Format

* A single non-negative integer `x`.

### 📤 Output Format

* A single integer, the **floor** value of the square root of `x`.

---

### 🧪 Sample Test Cases

#### Input 1:

```
4
```

#### Output 1:

```
2
```

#### Input 2:

```
8
```

#### Output 2:

```
2
```

> ✅ Because √8 ≈ 2.828..., and floor(√8) = **2**

---

### 🔍 Binary Search Approach (Efficient)

We find the square root using **Binary Search** between `0` and `x`.
At each step, we check if `mid * mid <= x`. If so, store `mid` as a possible answer and go right.

---

### 💻 Java Code (No Math.sqrt Used)

```java
import java.util.*;

class Maths {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int x = sc.nextInt();

        // Binary Search to find sqrt(x)
        int low = 0, high = x;
        int ans = 0;

        while (low <= high) {
            int mid = low + (high - low) / 2;

            // Use long to avoid overflow for mid*mid
            if ((long)mid * mid <= x) {
                ans = mid;        // Potential answer
                low = mid + 1;    // Try to find a bigger one
            } else {
                high = mid - 1;   // Mid too big
            }
        }

        System.out.println(ans);
    }
}
```

---

### ⏱ Time & Space Complexity

| Metric           | Value    |
| ---------------- | -------- |
| Time Complexity  | O(log x) |
| Space Complexity | O(1)     |

---

✅ This solution is safe from **integer overflow** and runs in **logarithmic time** even for large values of `x`.
