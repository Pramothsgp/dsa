# 🏢 Max Area Rectangle in Adjacent Buildings

## 🚩 Problem Statement

Given an array of positive integers representing the heights of adjacent buildings (all with width 1), **find the area of the largest rectangle** that can be formed using one or more adjacent buildings.

- **Width**: Number of buildings used.
- **Height**: Shortest building among the selected buildings.

---

## 📥 Input Format

A single line of **space-separated positive integers**, each representing a building's height.

## 📤 Output Format

A single integer: the **maximum area** of a rectangle that can be formed using adjacent buildings.

---

## ⛓️ Constraints

- `1 ≤ n ≤ 10⁴` &nbsp; *(number of buildings)*
- `1 ≤ heights[i] ≤ 10⁴` &nbsp; *(height of each building)*

---

## 🧪 Sample Test Cases

### Input 1
```
2 1 2
```
### Output 1
```
3
```

---

### Input 2
```
2 1 2 3 1 4 3 2 
```
### Output 2
```
8
```

---

## 💡 Java Solution

```java
import java.util.*;

class MaxArea {
    public static void main(String[] args) {
        // Read input as a line of space-separated integers
        String[] s = new Scanner(System.in).nextLine().trim().split("\\s+");
        int[] heights = new int[s.length];
        for (int i = 0; i < s.length; i++) {
            heights[i] = Integer.parseInt(s[i]);
        }
        // Output the maximum area
        System.out.println(findMaxArea(heights));
    }

    // Function to find the maximum rectangular area in the histogram
    private static int findMaxArea(int[] heights) {
        Stack<Integer> stack = new Stack<>();
        // Add a zero at the end to ensure all bars are processed
        int[] temp = Arrays.copyOf(heights, heights.length + 1);
        int res = 0;
        for (int i = 0; i < temp.length; i++) {
            // Maintain a stack of indices with increasing bar heights
            while (!stack.isEmpty() && temp[i] < temp[stack.peek()]) {
                int height = temp[stack.pop()]; // Height of the bar
                // Width is current index minus index of previous lower bar minus one
                int width = stack.isEmpty() ? i : i - stack.peek() - 1;
                res = Math.max(res, height * width); // Update max area
            }
            stack.push(i);
        }
        return res;
    }
}
```

---

> **Tip:** This is a classic stack-based problem, similar to finding the largest rectangle in a histogram!