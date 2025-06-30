# Two Sum

Given an array of integers `nums` and an integer `target`, return the indices of the two numbers such that they add up to `target`.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.

---

## Examples

**Example 1:**

```
Input: nums = 2 7 11 15 -1
    target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].
```

**Example 2:**

```
Input: nums = 3 0 -1
    target = 10
Output: No valid pair found.
```

**Example 3:**

```
Input: nums = 3 3
    target = 6
Output: [0,1]
```

---

## Input Format

- The first line of input consists of a sequence of integers representing the array, separated by spaces.
- The sequence ends with `-1` (which is not part of the array).
- The second line contains a single integer indicating the target value.

## Output Format

- If a valid pair is found that sums to the target, output the indices of the two elements as:
  ```
  [index1,index2]
  ```
- If no valid pair exists:
  ```
  No valid pair found.
  ```

Refer to the sample output for formatting specifications.

---

## Code Constraints

- 2 ≤ nums.length ≤ 10⁴
- -10⁹ ≤ nums[i] ≤ 10⁹
- -10⁹ ≤ target ≤ 10⁹
- Only one valid answer exists.

---

## Sample Test Cases

**Input 1:**
```
2 7 11 15 -1
9
```
**Output 1:**
```
[0,1]
```

**Input 2:**
```
3 0 -1  
10
```
**Output 2:**
```
No valid pair found.
```

---

## Java Implementation

```java
import java.util.*;

class TwoSum{
    public static void main(String[] args){
     Scanner sc = new Scanner(System.in);
     // Read the input line and split by spaces
     String s[] = sc.nextLine().trim().split(" ");
     int[] nums = new int[s.length];
     for(int i=0;i<nums.length;i++){
         nums[i] = Integer.parseInt(s[i]);
     }
     // Read the target value
     int target = sc.nextInt();
     // Use a HashMap to store value and its index
     Map<Integer,Integer> map = new HashMap<>();
     for(int i=0;i<nums.length;i++){
         // Check if the complement exists in the map
         if(map.containsKey(target - nums[i])){
          System.out.printf("[%d, %d]\n" , map.get(target - nums[i]) , i);
          return;
         } else{
          // Store the value and its index
          map.put(nums[i] , i);
         }
     }
     // If no valid pair is found
     System.out.println("No valid pair found.");
    }
}
```