## Next Greater Element in a Circular Array

Write a function that takes an array of integers and returns a new array where each element is the next greater element for that index, considering the array as circular.

### Problem Description

For each index `i` in the input array:

- Find the next element to the right (wrapping around to the start if needed) that is greater than `inputArray[i]`.
- If no such element exists, store `-1` at that position in the result.

### Circular Array Condition

The array is **circular**: after reaching the end, continue searching from the beginning.

#### Examples

- Input: `[1, 2]`  
    Output: `[2, -1]`

- Input: `[0, 0, 5, 0, 0, 3, 0, 0]`  
    The next greater element after `3` is `5` (wrapping around).  

### Input Format

- The first line contains an integer `n`, the number of elements in the array.
- The second line contains `n` space-separated integers, the elements of the array.

### Output Format

- Print a single line with `n` space-separated integers — the next greater element for each index.

### Constraints

- `1 ≤ n ≤ 10⁴`
- `-10⁹ ≤ array[i] ≤ 10⁹`

### Sample Test Cases

#### Input 1
```
3
1 3 2
```
#### Output 1
```
3 -1 3
```

#### Input 2
```
7
1 2 3 4 3 2 1
```
#### Output 2
```
2 3 4 -1 4 3 2
```

## Java Implementation

```java
import java.util.*;

class NextGreaterElement{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[] nums = new int[n];
        // Read the input array
        for(int i=0;i<n;i++){
            nums[i] = sc.nextInt();
        }
        int[] res = findNextGreaterNumber(nums);
        
        // Print the result array
        for(int num : res){
            System.out.printf("%d ", num);
        }
    }
    
    // Function to find the next greater element for each index in a circular array
    private static int[] findNextGreaterNumber(int[] nums){
        int n = nums.length;
        int[] res = new int[n];
        Arrays.fill(res , -1); // Initialize result array with -1
        
        Stack<Integer> stack = new Stack<>();
        // Traverse the array twice (simulate circular array)
        for(int i=2 * n - 1 ;i>=0;i--){
            int index = i % n; // Get the correct index in circular manner
            // Pop elements from stack while current element is greater or equal
            while(!stack.isEmpty() && nums[stack.peek()] <= nums[index]){
                stack.pop();
            }
            
            // If stack is not empty, the top element is the next greater
            if(!stack.isEmpty()){
                res[index] = nums[stack.peek()];
            }
            
            // Push current index onto stack
            stack.push(index);
        }
        
        return res;
    }
}
```