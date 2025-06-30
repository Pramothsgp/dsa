Given an integer array `nums` and an integer `val`, remove all occurrences of `val` in `nums` in-place. The order of the elements may be changed. Then return the number of elements in `nums` which are not equal to `val`.

Consider the number of elements in `nums` which are not equal to `val` be `k`. To get accepted, you need to do the following things:

- Change the array `nums` such that the first `k` elements of `nums` contain the elements which are not equal to `val`. The remaining elements of `nums` are not important as well as the size of `nums`.
- Return `k`.

---

### Example 1

**Input:**  
`nums = [3,2,2,3]`, `val = 3`

**Output:**  
`2, nums = [2,2,_,_]`

**Explanation:**  
Your function should return `k = 2`, with the first two elements of `nums` being `2`.  
It does not matter what you leave beyond the returned `k` (hence they are underscores).

---

### Example 2

**Input:**  
`nums = [0,1,2,2,3,0,4,2]`, `val = 2`

**Output:**  
`5, nums = [0,1,4,0,3,_,_,_]`

**Explanation:**  
Your function should return `k = 5`, with the first five elements of `nums` containing `0, 0, 1, 3, 4`.  
Note that the five elements can be returned in any order.  
It does not matter what you leave beyond the returned `k` (hence they are underscores).

---

### Input format

- The first line of input contains the array in the format: `[num1, num2, num3, ...]`.
- The second line of input contains the integer `val` (the element to be removed from the array).

### Output format

- The output prints an integer, representing the new length of the array after removing all instances of the given value, followed by the modified array in the format: `length, nums = [remaining elements]`
- Only the first `length` elements of the array should be printed in the result.

Refer to the sample output for formatting specifications.

---

### Code constraints

- `0 ≤ nums.length ≤ 100`
- `0 ≤ nums[i] ≤ 50`
- `0 ≤ val ≤ 100`

---

### Sample test cases

**Input 1:**  
```
[3, 2, 2, 3]
3
```
**Output 1:**  
```
2, nums = [2, 2]
```

**Input 2:**  
```
[0, 1, 2, 2, 3, 0, 4, 2]
2
```
**Output 2:**  
```
5, nums = [0, 1, 3, 0, 4]
```

---
## Java

```java []
import java.util.*;

class RemoveElement {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        // Read the input array as a string, remove brackets and spaces, then split by comma
        String[] s = sc.nextLine().replaceAll("\\[|\\]|\\s++", "").split(",");
        int[] nums = new int[s.length];
        // Convert the string array to an integer array
        for (int i = 0; i < nums.length; i++) {
            nums[i] = Integer.parseInt(s[i]);
        }
        // Read the target value to remove
        int target = sc.nextInt();
        int i = 0;
        // Iterate through the array and keep elements not equal to target
        for (int j = 0; j < nums.length; j++) {
            if (nums[j] != target) {
                nums[i++] = nums[j];
            }
        }
        // Build the output string for the modified array
        StringBuilder sb = new StringBuilder("[");
        for (int j = 0; j < i; j++) {
            sb.append(nums[j]);
            if (j != i - 1) {
                sb.append(", ");
            }
        }
        sb.append("]");
        // Print the result: new length and modified array
        System.out.printf("%d, nums = %s", i, sb.toString());
    }
}
```