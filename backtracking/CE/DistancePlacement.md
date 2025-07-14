# 🧩 Distance-Constrained Duplicate Placement

### ✅ Problem Statement

Given a number `n`, construct an array of size `2n` containing **two instances of every number** from `1` to `n`, such that:

> For any number `i`, there are exactly `i` **elements between the two occurrences** of `i`.

If such a configuration is **not possible**, print `"Not Possible"`.

---

### 🧾 Input Format

* A single integer `n`

---

### 📤 Output Format

* A list of integers (space-separated), if a valid arrangement exists
* Otherwise, print:

  ```
  Not Possible
  ```

---

### 🧪 Sample Test Cases

#### Input 1:

```
3
```

#### Output 1:

```
3 1 2 1 3 2 
```

#### Input 2:

```
4
```

#### Output 2:

```
4 1 3 1 2 4 3 2 
```

#### Input 3:

```
2
```

#### Output 3:

```
Not Possible
```

---

### 💡 Explanation

For a number `i`, the second occurrence must be placed at a distance of exactly `i + 1` indices from the first.

For example:

* For `i = 3`, if the first `3` is at index `0`, the second `3` must be at `0 + 3 + 1 = 4`.
* The resulting array must satisfy this rule for **all numbers from `1` to `n`**.

We solve this using **backtracking**.

---

### 🔁 Java Backtracking Solution

```java
import java.util.*;

public class DistancePlacement {
    static int[] result;
    static boolean[] used;
    static int n;
    static boolean solved = false;

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        n = sc.nextInt();
        result = new int[2 * n];

        if (placeNumbers(n)) {
            for (int num : result) System.out.print(num + " ");
        } else {
            System.out.println("Not Possible");
        }
    }

    /**
     * Attempts to place numbers from 'num' to '1' into the result array
     * such that the distance condition is maintained.
     */
    private static boolean placeNumbers(int num) {
        // Base case: all numbers placed
        if (num <= 0) return true;

        for (int i = 0; i + num + 1 < 2 * n; i++) {
            // Check if both required positions are empty
            if (result[i] == 0 && result[i + num + 1] == 0) {
                result[i] = num;
                result[i + num + 1] = num;

                if (placeNumbers(num - 1)) return true;

                // Backtrack
                result[i] = 0;
                result[i + num + 1] = 0;
            }
        }

        return false;
    }
}
```

---

### ⏱️ Time Complexity

* Worst-case is exponential due to backtracking
* Efficient for `n ≤ 20` as required

---

### 📌 Notes

* There may be multiple valid arrangements; any one is acceptable.
* The problem is known as the **Langford Pairing Problem**, solvable only when `n % 4 == 0` or `n % 4 == 3`.

---
