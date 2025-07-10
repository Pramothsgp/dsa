# 📦 Factory Warehouse Shelf Organizer

## 🧩 Problem Statement

You are organizing a set of **boxes in a factory warehouse**. Each box acts as a **shelf**, and products are represented by **balls**. Your task is to gather **all products onto a single shelf**, but you must compute the **minimum number of operations** required to gather all products to **each shelf individually**.

* A product can only be moved to an **adjacent shelf**.
* A shelf containing `'1'` has a product, and `'0'` is empty.

Your goal is to calculate, for **each shelf**, the **minimum total moves** needed to gather all the products onto that particular shelf.

---

## 📥 Input Format

* A single line containing a binary string (only `'0'` and `'1'`).

  * `'1'` represents a shelf with a product.
  * `'0'` represents an empty shelf.

---

## 📤 Output Format

* Print **space-separated integers**.
* Each number represents the **minimum number of operations** required to move all balls to that corresponding shelf.

---

## 🔒 Constraints

* `1 ≤ length of the string ≤ 100`
* Input contains only `'1'` or `'0'`.

---

## 🧪 Sample Test Cases

### ✅ Sample Input 1:

```
001011
```

### ✅ Sample Output 1:

```
11 8 5 4 3 4
```

### ✅ Sample Input 2:

```
110
```

### ✅ Sample Output 2:

```
1 1 3
```

---

## 💡 Explanation

Let's walk through input `110`:

* **Box 0**: Move ball from box 1 → needs 1 move → total = 1
* **Box 1**: Move ball from box 0 → needs 1 move → total = 1
* **Box 2**: Move ball from box 0 (2 moves) and box 1 (1 move) → total = 3

---

## 💻 Java Code Implementation

```java
import java.util.*;

class StepCount {
    public static void main(String[] args) {
        String s = new Scanner(System.in).nextLine();  // 🟡 Read input string
        int n = s.length();                            // 🔢 Length of the string
        int steps = 0, balls = 0;

        int[] leftSteps = new int[n];   // ⬅️ Steps needed from the left
        int[] rightSteps = new int[n];  // ➡️ Steps needed from the right

        // 🔁 First Pass: Left to Right
        for (int i = 0; i < n; i++) {
            leftSteps[i] = steps;
            if (s.charAt(i) == '1') balls++;
            steps += balls;
        }

        // 🔁 Second Pass: Right to Left
        steps = balls = 0;
        for (int i = n - 1; i >= 0; i--) {
            rightSteps[i] = steps;
            if (s.charAt(i) == '1') balls++;
            steps += balls;
        }

        // 🖨️ Print the final result
        for (int i = 0; i < n; i++) {
            System.out.printf("%d ", leftSteps[i] + rightSteps[i]);
        }
    }
}
```

---

## 🏁 Output Explanation:

Each value in the output indicates how many **minimal steps** are needed to move all balls to the corresponding box.

---
