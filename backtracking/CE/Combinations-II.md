# 🧩 Problem: Unique Gift Combinations (Backtracking)

### 💡 Problem Statement

Imagine you're helping a friend plan **gift packages** with a **total budget of `N`**. Your task is to find all **unique ways** to spend the **entire budget** on different combinations of gift prices, ensuring **no combination is repeated** by rearranging the prices.

### 📌 Rules:

* All combinations must **sum to `N`**.
* Combinations must be in **non-decreasing order** (e.g., `[1, 2, 1]` becomes `[1, 1, 2]`).
* No **permutation duplicates** allowed (e.g., `[1, 1, 2]` and `[2, 1, 1]` count as the same).
* All outputs must be printed in **lexicographical order**.

---

### 🧾 Input Format

* A single integer `n` (1 ≤ n ≤ 25) — the total budget to break down.

---

### 📤 Output Format

* A list of lists where each inner list contains integers summing up to `n`, printed in **lexicographically sorted** order.

---

### 📈 Constraints

* 1 ≤ N ≤ 25

---

### 📥 Sample Input 1

```
1
```

### 📤 Sample Output 1

```
[[1]]
```

---

### 📥 Sample Input 2

```
4
```

### 📤 Sample Output 2

```
[[1, 1, 1, 1], [1, 1, 2], [1, 3], [2, 2], [4]]
```

---

### 📥 Sample Input 3

```
3
```

### 📤 Sample Output 3

```
[[1, 1, 1], [1, 2], [3]]
```

---

### 🧠 Explanation

You are generating all **partitions of `N`** such that:

* Each partition is a list of integers summing to `N`.
* Integers are added in **non-decreasing order** to avoid duplicate permutations.
* For example, for `N = 4`, combinations like `[1, 3]` and `[3, 1]` are considered **the same**, and only one (in sorted form) is included.

---

### 🧮 Approach

We use **backtracking** to explore every possible combination:

1. Start from number `1` up to `n`.
2. Keep track of the current sum and path (`List<Integer>`).
3. Ensure that the next number we choose is **greater than or equal to the previous** to maintain non-decreasing order.
4. When the sum reaches `n`, add the current list to the result.

---

### ✅ Java Code with Comments

```java
import java.util.*;

class Combinations {
    // Global list to store all valid combinations
    static List<List<Integer>> res;

    public static void main(String[] args) {
        // Read input from the user
        int n = new Scanner(System.in).nextInt();

        // Initialize the result list
        res = new ArrayList<>();

        // Start backtracking from number 1
        backtrack(n, 0, new ArrayList<>(), 1);

        // Print all valid combinations
        System.out.println(res);
    }

    /**
     * Recursive backtracking method
     * 
     * @param n   Target sum
     * @param sum Current sum being built
     * @param cur Current combination being built
     * @param num The smallest number we can use next
     */
    private static void backtrack(int n, int sum, List<Integer> cur, int num) {
        // Base case: if current sum equals target, store the result
        if (sum == n) {
            res.add(new ArrayList<>(cur));
            return;
        }

        // If current sum exceeds the target, stop further recursion
        if (sum > n) return;

        // Try adding numbers from 'num' to 'n' to ensure non-decreasing order
        for (int i = num; i <= n; i++) {
            cur.add(i); // Choose the number
            backtrack(n, sum + i, cur, i); // Explore further with updated sum
            cur.remove(cur.size() - 1); // Backtrack and try next option
        }
    }
}
```

---

### 🧪 Time Complexity (Approximate)

* The problem is similar to **integer partition**, and the number of such partitions grows **exponentially** with `n`.
* Time Complexity: `O(2^n)` (rough upper bound)
* Space Complexity: `O(n)` (due to recursion depth and list storage)

---

