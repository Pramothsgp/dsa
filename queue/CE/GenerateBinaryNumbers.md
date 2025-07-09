# 🔢 Generating Binary Numbers from 1 to *n* using a Queue in Java

Sneha is passionate about binary numbers and wants to **visualize their sequential evolution** from `1` to a given number `n`. This Java program uses a **queue-based approach** to generate binary numbers efficiently.

---

## 📌 Problem Statement

* Given an integer `n`, generate the binary representation of numbers from `1` to `n`.
* Use a **queue** to ensure sequential generation in **binary tree level-order fashion**.

---

## 🧾 Input Format

* A single integer `n`
  (1 ≤ `n` ≤ 20)

---

## 🖨️ Output Format

```
Binary numbers from 1 to n are:
<binary1>
<binary2>
...
<binaryN>
```

---

## 📍 Sample Input 1

```
3
```

### ✅ Sample Output 1

```
Binary numbers from 1 to 3 are:
1
10
11
```

## 📍 Sample Input 2

```
5
```

### ✅ Sample Output 2

```
Binary numbers from 1 to 5 are:
1
10
11
100
101
```

---

## ✅ Java Code with Explanation

```java
import java.util.*;

class BinaryNumbers {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // Read the value of n
        int n = sc.nextInt();

        // Initialize a queue to hold binary numbers as strings
        Queue<String> q = new LinkedList<>();

        // Start with "1" in the queue
        q.offer("1");

        // Print heading as required
        System.out.printf("Binary numbers from 1 to %d are:\n", n);

        // Generate binary numbers from 1 to n using BFS
        for (int i = 0; i < n; i++) {
            // Fetch the front binary number
            String cur = q.poll();

            // Print current binary number
            System.out.println(cur);

            // Append '0' and '1' to form next binary numbers
            q.offer(cur + "0");
            q.offer(cur + "1");
        }
    }
}
```

---

## 🧠 Key Concepts Used

| Concept             | Explanation                                                        |
| ------------------- | ------------------------------------------------------------------ |
| Queue               | FIFO structure ensures binary numbers are generated level by level |
| String Manipulation | Build new binary numbers by appending `0` and `1`                  |
| BFS-like Expansion  | Mimics traversal of a binary tree in level order                   |

---
