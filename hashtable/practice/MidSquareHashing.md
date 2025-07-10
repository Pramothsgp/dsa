# 📦 Hash Table using Mid-Square Method with Linear Probing

## 👨‍💻 Scenario

Akil, a computer science student, is exploring **hash tables** and wants to implement a collision resolution strategy using:

* 📐 **Mid-square hashing**
* ➕ **Linear probing**

The hash table has a **fixed size of 100**, and the goal is to **insert keys** efficiently while handling collisions.

---

## 🧠 Hashing Strategy

### 🔸 Mid-Square Hashing Method

1. **Square the key**.
2. Divide the result by **10**.
3. Take the **remainder modulo 100**.
4. Then take modulo **TABLE\_SIZE (100)** to get the index.

### 🔸 Collision Handling: Linear Probing

If the computed index is **occupied**, we search for the **next available index** (in a circular manner).

---

## 📥 Input Format

* First line: An integer `n` → number of keys to insert.
* Second line: `n` space-separated integers → the keys.

## 📤 Output Format

* For each key inserted, print:
  `Index x: Key y`

---

## 🧪 Sample Input 1:

```
5
80 65 40 60 98
```

## ✅ Sample Output 1:

```
Index 22: Key 65
Index 40: Key 80
Index 60: Key 40
Index 61: Key 60
Index 62: Key 98
```

---

## 🔍 Explanation

* **Key 80** → 80² = 6400 → 640 → 640 % 100 = **40**
* **Key 65** → 65² = 4225 → 422 → 422 % 100 = **22**
* **Key 40** → 40² = 1600 → 160 → 160 % 100 = **60**
* **Key 60** → 60² = 3600 → 360 → 360 % 100 = **60** → Collision → next is **61**
* **Key 98** → 98² = 9604 → 960 → 960 % 100 = **60** → Collision → next: 61, 62 → Insert at **62**

---

## 💻 Java Code Implementation

```java
import java.util.*;

public class HashTableMidSquare {
    static final int TABLE_SIZE = 100;

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt();               // Number of keys
        int[] keys = new int[n];
        int[] hashTable = new int[TABLE_SIZE];
        Arrays.fill(hashTable, -1);         // Initialize table with -1 (empty)

        // Read keys
        for (int i = 0; i < n; i++) {
            keys[i] = sc.nextInt();
        }

        for (int i = 0; i < n; i++) {
            int key = keys[i];
            int square = key * key;
            int midDigits = (square / 10) % 100;         // Extract middle digits
            int index = midDigits % TABLE_SIZE;

            // Linear probing for collision resolution
            while (hashTable[index] != -1) {
                index = (index + 1) % TABLE_SIZE;
            }

            hashTable[index] = key;
            System.out.println("Index " + index + ": Key " + key);
        }
    }
}
```

---

## 📌 Constraints

* Hash table size = **100**
* `1 ≤ n ≤ 10`
* `10 ≤ key ≤ 100`

---
