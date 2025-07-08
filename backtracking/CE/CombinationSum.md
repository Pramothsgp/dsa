# 🧮 Combination Sum (With Repetition)

## 📝 Problem Statement

Given an array of **positive integers** and a **target sum `B`**, find all **unique combinations** in the array where the **sum equals `B`**.

* A number from the array **can be used multiple times**.
* The elements in each combination must be in **non-descending order**.
* The combinations themselves must be sorted in **ascending order**.

---

## 📥 Input Format

* The **first line** contains space-separated positive integers — the elements of the array.
* The **second line** contains an integer `B` — the target sum.

## 📤 Output Format

Print:

```
Combinations that sum to B are:
( a1 a2 ... ak ) ( b1 b2 ... bn ) ...
```

Each combination is enclosed in parentheses and sorted in non-descending order. Combinations themselves are sorted in ascending lexicographic order.

---

## ✅ Constraints

* `1 ≤ arr[i] ≤ 10`
* `1 ≤ B ≤ 25`

---

## 💡 Sample Test Case 1

### Input

```
7 2 6 5
16
```

### Output

```
Combinations that sum to 16 are:
( 2 2 2 2 2 2 2 2 ) ( 2 2 2 2 2 6 ) ( 2 2 2 5 5 ) ( 2 2 5 7 ) ( 2 2 6 6 ) ( 2 7 7 ) ( 5 5 6 ) 
```

### Explanation

You can use any number any number of times. All valid combinations that sum to `16` include combinations of `2`s, `5`s, `6`s, and `7`s.

---

## 💡 Sample Test Case 2

### Input

```
6 5 7 1 8 2 9 9 7 7 9
6
```

### Output

```
Combinations that sum to 6 are:
( 1 1 1 1 1 1 ) ( 1 1 1 1 2 ) ( 1 1 2 2 ) ( 1 5 ) ( 2 2 2 ) ( 6 ) 
```

---

## 💡 Sample Test Case 3

### Input

```
2 4 6 8
8
```

### Output

```
Combinations that sum to 8 are:
( 2 2 2 2 ) ( 2 2 4 ) ( 2 6 ) ( 4 4 ) ( 8 ) 
```

---

## 🧑‍💻 Java Code Implementation

```java
import java.util.*;

public class Main {

    // Function to find and print all unique combinations that sum to the target
    private static void findCombinations(int[] nums, int target) {
        // Use a Set to remove duplicates from input array
        Set<Integer> set = new HashSet<>();
        for (int num : nums) {
            set.add(num);
        }

        // Convert Set back to List and initialize result container
        List<Integer> list = new ArrayList<>(set);
        List<List<Integer>> res = new ArrayList<>();

        // Begin backtracking from index 0
        backtrack(res, list, new ArrayList<Integer>(), target, 0);

        // Print the results in the required format
        System.out.printf("Combinations that sum to %d are:\n", target);
        for (List<Integer> comb : res) {
            System.out.print("( ");
            for (int val : comb) {
                System.out.printf("%d ", val);
            }
            System.out.print(") ");
        }
    }

    // Backtracking function to generate combinations
    private static void backtrack(List<List<Integer>> res, List<Integer> list, List<Integer> cur, int target, int index) {
        // Base case: if target is met, add current combination to result
        if (target == 0) {
            res.add(new ArrayList<>(cur));
            return;
        }

        // If target goes below zero, stop exploring this path
        if (target < 0) {
            return;
        }

        // Explore all candidates starting from current index (allows reuse of same element)
        for (int i = index; i < list.size(); i++) {
            cur.add(list.get(i));  // Choose
            backtrack(res, list, cur, target - list.get(i), i);  // Explore
            cur.remove(cur.size() - 1);  // Un-choose (Backtrack)
        }
    }

    // Main method to read input and invoke the logic
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        // Read array elements from input
        String[] input = scanner.nextLine().trim().split("\\s+");
        int[] arr = new int[input.length];
        for (int i = 0; i < input.length; i++) {
            arr[i] = Integer.parseInt(input[i]);
        }

        // Read target sum
        int target = scanner.nextInt();

        // Call the combination finder
        findCombinations(arr, target);

        scanner.close();
    }
}
```

---

## 📌 Notes

* The backtracking algorithm builds combinations by recursively adding elements.
* The same element can be reused by passing the **same index** again.
* Duplicates are removed using a `Set` to ensure combinations are **unique**.
* The result list is printed in the format required by the problem.
