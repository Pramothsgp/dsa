# 🧩 Problem Statement

The **Robotics Research Division** of IIT TechFest challenges teams to **maximize vertical space** in a warehouse using disks of **unique dimensions** (`width`, `depth`, `height`).

Your task is to:

* Stack disks on top of each other.
* A disk **can only be placed on another** if its **width, depth, and height are all strictly smaller**.
* **Disks cannot be rotated**.

🔍 **Goal**: Return the **tallest possible stack** (in terms of total height), and print the disks **from top to bottom**.

---

## ✅ Input Format

```
Line 1: Integer n → Number of disks

Next n lines: Each line has 3 integers → width depth height
```

## ✅ Output Format

```
Each line prints a disk's dimensions from top to bottom of the final stack:
width depth height
```

---

## ✅ Constraints

* 1 ≤ n ≤ 100
* 1 ≤ width, depth, height ≤ 100
* All disks have **unique dimensions**

---

## ✅ Sample Input 1

```
3
1 1 1
2 2 2
3 3 3
```

### ✅ Output 1

```
1 1 1
2 2 2
3 3 3
```

**Explanation**: Each disk is smaller in all 3 dimensions than the next one, so we can stack all 3.

---

## ✅ Sample Input 2

```
5
2 2 1
3 3 4
2 1 2
4 4 5
1 1 1
```

### ✅ Output 2

```
2 1 2
3 3 4
4 4 5
```

**Explanation**:

* Valid sequence: 2 1 2 → 3 3 4 → 4 4 5
* Tallest stack with increasing dimensions.

---

## ✅ Java Code (Unchanged) — With Explanation in Comments

```java
import java.util.*;

class LongestIncreasingSubSequence3D {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[][] disks = new int[n][3];

        // Reading all disks
        for (int i = 0; i < n; i++) {
            disks[i][0] = sc.nextInt(); // width
            disks[i][1] = sc.nextInt(); // depth
            disks[i][2] = sc.nextInt(); // height
        }

        // Sort disks by height (ascending)
        Arrays.sort(disks, Comparator.comparingInt(a -> a[2]));

        int[] heights = new int[n]; // max stack height ending at i
        for (int i = 0; i < n; i++) {
            heights[i] = disks[i][2]; // initially, height is the disk itself
        }

        int[] prev = new int[n]; // tracks previous disk in the stack
        Arrays.fill(prev, -1); // initialize to -1 (no previous disk)

        int index = 0; // tracks index of disk with tallest stack

        for (int i = 1; i < n; i++) {
            for (int j = 0; j < i; j++) {
                // If disk[j] can go below disk[i]
                if (disks[j][0] < disks[i][0] && disks[j][1] < disks[i][1] && disks[j][2] < disks[i][2]) {
                    // Update height if it's better to include disk[j] below disk[i]
                    if (heights[i] < heights[j] + disks[i][2]) {
                        heights[i] = heights[j] + disks[i][2];
                        prev[i] = j;
                    }
                }
            }
            // Track max height stack ending at index i
            if (heights[i] > heights[index]) {
                index = i;
            }
        }

        // Build the stack from bottom to top using `prev[]`
        Stack<int[]> stack = new Stack<>();
        while (index != -1) {
            stack.add(disks[index]);
            index = prev[index];
        }

        // Print stack from top to bottom
        while (!stack.isEmpty()) {
            int[] cur = stack.pop();
            System.out.printf("%d %d %d\n", cur[0], cur[1], cur[2]);
        }
    }
}
```

---

## 🧠 Time & Space Complexity

| Aspect         | Complexity |
| -------------- | ---------- |
| Sorting        | O(n log n) |
| DP comparison  | O(n²)      |
| Space (arrays) | O(n)       |
| Output (stack) | O(n)       |

---
