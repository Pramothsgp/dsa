# 🤖 Robot Navigation System — Single Cycle Check

## 🧩 Problem Statement

You are designing a **robotic navigation system** for a **circular training track**.
The track is divided into segments forming a **circular array**, and each segment contains a **jump instruction**:

* A **positive number** → move forward
* A **negative number** → move backward
* **Jumps wrap** around the circular track

### 🎯 Objective

Determine whether the **jump instructions form a single complete cycle**, meaning:

* ✅ Every segment is **visited exactly once**
* ✅ The robot **returns to the starting segment (0)** after exactly `n` steps

---

## 📝 Input Format

```
Line 1: An integer n — number of segments (1 ≤ n ≤ 10⁵)  
Line 2: n space-separated integers — jump instructions (−n ≤ a[i] ≤ n)
```

## 🖨️ Output Format

```
Print "true" if a valid single cycle exists  
Otherwise, print "false"
```

---

## 🧪 Sample Test Cases

### Input 1:

```
6
2 3 1 -4 -4 2
```

### Output 1:

```
true
```

### Input 2:

```
5
1 2 3 4 -2
```

### Output 2:

```
false
```

---

## 👨‍💻 Java Code with Explanation

```java
import java.util.*;

class RobotNavigation {

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // 🔢 Read number of segments
        int n = sc.nextInt();

        // 📥 Read jump instructions into array
        int[] steps = new int[n];
        for (int i = 0; i < n; i++) {
            steps[i] = sc.nextInt();
        }

        // ✅ Print result: whether the path is a single complete cycle
        System.out.println(hasUniquePath(steps));
    }

    /**
     * 🚀 Function to check if robot visits every segment exactly once
     * and returns back to the starting point after n steps
     */
    private static boolean hasUniquePath(int[] steps) {
        int n = steps.length;

        // 🔍 Track visited segments
        boolean[] visited = new boolean[n];

        // 🧭 Start from segment 0
        int current = 0;
        int count = 0;

        // 🌀 Perform n jumps
        while (count < n) {
            // ⚠️ Already visited — invalid cycle
            if (visited[current]) return false;

            visited[current] = true; // ✅ Mark current as visited
            count++;

            // ➡️ Move to next segment (with wrapping)
            current = nextIndex(current, steps[current], n);
        }

        // ✅ After n steps, robot must return to start
        return current == 0;
    }

    /**
     * 🔄 Utility to get next index with circular wrapping
     */
    private static int nextIndex(int current, int jump, int n) {
        int next = (current + jump) % n;

        // 🧷 Adjust for negative modulo result
        return next >= 0 ? next : next + n;
    }
}
```

---

## 📌 How It Works

* Start at **index 0**
* Keep track of visited positions
* After `n` moves:

  * All `n` positions must be **visited exactly once**
  * Must land back at **index 0**
* If either condition fails — return `"false"`

---

## 🧠 Time & Space Complexity

* ⏱ **Time:** O(n) — Each segment is visited once
* 🧠 **Space:** O(n) — Boolean array to track visited segments

---
