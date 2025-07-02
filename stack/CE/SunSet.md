Problem Statement:

Given an array of building heights and a direction that all buildings face ("EAST" or "WEST"), determine which buildings can see the sunset.

A building can see the sunset if it is strictly taller than all buildings that come after it in the direction it faces.

- When buildings face **"EAST"** → check rightward.
- When buildings face **"WEST"** → check leftward.

**Input format:**

- `n` is the number of buildings.
- `h1 h2 ... hn` are the space-separated heights of the buildings.
- `direction` is a string: "EAST" or "WEST".

**Output format:**

- Output indices must be in ascending order, regardless of the traversal direction.

**Code constraints:**

- `1 ≤ n ≤ 10^5`
- `1 ≤ hi ≤ 10^6` (where hi is the height of the i-th building)
- `direction` {"EAST" or "WEST"}
- All buildings face the same direction.
- Building heights are positive and non-zero integers.
- Output indices must be in increasing (ascending) order, regardless of traversal logic.

**Sample test cases:**

```
Input 1:
3
4 2 3
WEST

Output 1:
Buildings with sunset views: 0
```

```
Input 2:
8
3 5 4 4 3 1 3 2
EAST

Output 2:
Buildings with sunset views: 1 3 6 7
```

---

## Java Implementation

```java
import java.util.*;

class SunSet {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[] nums = new int[n];
        // Read building heights
        for (int i = 0; i < n; i++) {
            nums[i] = sc.nextInt();
        }

        String direction = sc.next();
        // Check direction and call appropriate method
        if (direction.equals("WEST")) {
            findBuildingsWest(nums);
        } else if (direction.equals("EAST")) {
            findBuildingsEast(nums);
        }
    }

    // Find buildings with sunset view when facing WEST
    private static void findBuildingsWest(int[] buildings) {
        Stack<Integer> stack = new Stack<>();
        List<Integer> res = new ArrayList<>();
        for (int i = 0; i < buildings.length; i++) {
            // If stack is empty or current building is taller than previous
            if (stack.isEmpty() || stack.peek() < buildings[i]) {
                res.add(i);
                stack.push(buildings[i]);
            }
        }

        System.out.print("Buildings with sunset views: ");
        for (int a : res) {
            System.out.printf("%d ", a);
        }
    }

    // Find buildings with sunset view when facing EAST
    private static void findBuildingsEast(int[] buildings) {
        Stack<Integer> stack = new Stack<>();
        List<Integer> res = new ArrayList<>();
        for (int i = buildings.length - 1; i >= 0; i--) {
            // If stack is empty or current building is taller than previous
            if (stack.isEmpty() || stack.peek() < buildings[i]) {
                res.add(i);
                stack.push(buildings[i]);
            }
        }
        // Reverse to maintain ascending order of indices
        Collections.reverse(res);
        System.out.print("Buildings with sunset views: ");
        for (int a : res) {
            System.out.printf("%d ", a);
        }
    }
}
```
