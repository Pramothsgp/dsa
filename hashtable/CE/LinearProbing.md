# 🧠 Problem: Implementing Hash Table with Linear Probing

**Sindhu** is working on implementing a **hash table** using **linear probing** to store a set of unique integers efficiently. You are to help her by developing a program that:

* Uses the **division method** for hashing.
* Resolves collisions using **linear probing**.
* Outputs the final key positions in **ascending index order**.

---

### 📥 Input Format:

```
Line 1: Integer m → size of the hash table  
Line 2: Integer n → number of keys to insert  
Line 3: n space-separated integers → the keys to be inserted  
```

---

### 📤 Output Format:

```
Each line in the format:
index: [index], value: [value]
Only for occupied indices (in ascending index order)
```

---

### ✅ Constraints:

* 1 ≤ m ≤ 10
* 1 ≤ n ≤ 10
* 1 ≤ key ≤ 100

---

### 🔍 Sample Input 1:

```
5
5
14 16 17 26 10
```

### 📌 Sample Output 1:

```
index: 0, value: 10
index: 1, value: 16
index: 2, value: 17
index: 3, value: 26
index: 4, value: 14
```

---

### 🧾 Explanation:

* Hash function used: `index = (key + j) % m` where `j` is the number of probes.
* Collision is resolved using linear probing by checking the next index `(index + 1)`, `(index + 2)`, etc.
* Keys are stored in the hash table and printed based on their final stored index.

---

### 💻 Java Code with Comments:

```java
import java.util.*;

class HashTable {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // Read size of the hash table
        int m = sc.nextInt();

        // Read number of elements to be inserted
        int n = sc.nextInt();

        // Create and initialize the hash table with -1 (indicates empty)
        int[] hashtable = new int[m];
        Arrays.fill(hashtable, -1);

        // Insert each key into the hash table using linear probing
        for (int i = 0; i < n; i++) {
            int val = sc.nextInt(); // Read the key to insert

            // Try inserting using linear probing
            for (int j = 0; j < m; j++) {
                int index = (val + j) % m; // Division method + linear probe

                if (hashtable[index] == -1) {
                    hashtable[index] = val; // Insert the key
                    break; // Move to next key
                }
            }
        }

        // Print the final hash table contents in ascending index order
        for (int i = 0; i < m; i++) {
            if (hashtable[i] != -1) {
                System.out.printf("index: %d, value: %d\n", i, hashtable[i]);
            }
        }
    }
}
```

---
