
## 🎯 Combination Sum II

---

### 📝 Problem Statement

You are given a list of integers `candidates` and an integer `target`.
Find **all unique combinations** in `candidates` where the **sum is equal to target**.

* **Each number may only be used once per combination.**
* The result **must not contain duplicate combinations**.

---

### 📥 Input Format

* First line: space-separated integers → `candidates`
* Second line: an integer → `target`

### 📤 Output Format

* One valid combination per line in the format `[num1, num2, ...]`

---

### 🧪 Sample Test Cases

#### Input 1:

```
10 1 2 7 6 1 5
8
```

#### Output 1:

```
[1, 1, 6]
[1, 2, 5]
[1, 7]
[2, 6]
```

#### Input 2:

```
2 5 2 1 2
5
```

#### Output 2:

```
[1, 2, 2]
[5]
```

---

### 💡 Explanation

* Use **Backtracking** to explore combinations.
* **Sort** the array first to:

  * Prune when number > target
  * **Skip duplicates** using: `if (i > index && nums[i] == nums[i-1]) continue`

---

### 💻 Java Code (Single File)

```java
import java.util.*;

class CombinationSum {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // Read input array
        String[] s = sc.nextLine().split("\\s+");
        int[] nums = new int[s.length];
        for (int i = 0; i < nums.length; i++) {
            nums[i] = Integer.parseInt(s[i]);
        }

        // Read target value
        int target = sc.nextInt();

        // Sort to handle duplicates easily
        Arrays.sort(nums);

        // Start backtracking
        combinations(0, target, nums, new ArrayList<>());
    }

    // Backtracking function
    private static void combinations(int index, int target, int[] nums, List<Integer> res) {
        if (target == 0) {
            System.out.println(res);
            return;
        }

        for (int i = index; i < nums.length && nums[i] <= target; i++) {
            // Skip duplicates
            if (i > index && nums[i] == nums[i - 1]) continue;

            res.add(nums[i]);
            combinations(i + 1, target - nums[i], nums, res); // Move to next index (i + 1)
            res.remove(res.size() - 1); // Backtrack
        }
    }
}
```

---

### ⏱ Time & Space Complexity

| Metric           | Value                             |
| ---------------- | --------------------------------- |
| Time Complexity  | O(2^n), exponential in worst case |
| Space Complexity | O(target) recursive stack         |

---
