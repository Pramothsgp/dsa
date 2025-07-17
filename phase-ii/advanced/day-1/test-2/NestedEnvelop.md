
## 📦 Russian Doll Envelopes

---

### ✅ Problem Statement

You're given a list of `N` envelopes where each envelope has a **width** and **height**.
An envelope can fit into another **only if** both its width and height are strictly smaller.

> Your task is to find the **maximum number of envelopes** you can nest (like Russian dolls).

---

### 📥 Input Format

* First line: Integer `N` — number of envelopes
* Next `N` lines: Two integers per line — `wi` and `hi`

### 📤 Output Format

* A single integer — maximum number of envelopes that can be nested

---

### 🔁 Sample Input & Output

#### Input 1:

```
3
1 1
1 1
1 1
```

#### Output 1:

```
1
```

#### Input 2:

```
4
5 4
6 4
6 7
2 3
```

#### Output 2:

```
3
```

---

### 💡 Key Idea

* Sort envelopes by **width ascending**, but **height descending** when width is equal.
* Then apply **Longest Increasing Subsequence (LIS)** on the **height**.

---

### ✅ Java Code (Corrected)

```java
import java.util.*;

class NestedEnvelopes {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[][] env = new int[n][2];

        for (int i = 0; i < n; i++) {
            env[i][0] = sc.nextInt(); // width
            env[i][1] = sc.nextInt(); // height
        }

        // Sort: width asc, height desc (for same width)
        Arrays.sort(env, (a, b) -> {
            if (a[0] == b[0]) return b[1] - a[1];
            return a[0] - b[0];
        });

        // Apply Longest Increasing Subsequence on height
        List<Integer> lis = new ArrayList<>();

        for (int[] envelope : env) {
            int h = envelope[1];
            int idx = Collections.binarySearch(lis, h);
            if (idx < 0) idx = -(idx + 1);
            if (idx == lis.size()) {
                lis.add(h);
            } else {
                lis.set(idx, h);
            }
        }

        System.out.println(lis.size());
    }
}
```

---

### 🧠 Why This Works

* Sorting width ascending and height descending ensures no duplicate width envelopes are wrongly nested.
* After sorting, only height needs to be checked using LIS (like 1D nesting).

---

### ⏱ Time Complexity

* Sorting: `O(n log n)`
* LIS (via binary search): `O(n log n)`
* **Total**: `O(n log n)`

---

### ❌ Provided Java Code (Incorrect for general cases)

```java
import java.util.*;

class NestedEnvelopes {
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[][] env = new int[n][2];
        for(int i = 0; i < n; i++){
            env[i][0] = sc.nextInt();
            env[i][1] = sc.nextInt();
        }

        Arrays.sort(env, Comparator.comparingInt(a -> a[0]));

        int cnt = 1;
        int[] prev = env[0];
        for(int i = 1; i < n; i++){
            if(prev[0] < env[i][0] && prev[1] < env[i][1]){
                cnt++;
                prev = env[i];
            }
        }
        System.out.println(cnt);
    }
}
```

---

### ⚠️ What's Wrong in the Provided Code?

* It **only tracks the current pair** and greedily counts if next envelope is bigger — this doesn't work for all combinations.
* It **misses longer subsequences** like the correct LIS approach would find.
* It also **sorts only by width**, which may cause incorrect nesting when widths are equal.


---
}