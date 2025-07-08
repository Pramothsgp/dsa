## MinMaxStack Design

Design a `MinMaxStack` class that functions like a standard stack but also allows retrieving the current minimum and maximum values in constant time.

### Supported Operations

- `push x` — Push integer `x` onto the stack.
- `pop` — Remove the top element from the stack.
- `peek` — Return the top element without removing it.
- `getMin` — Return the minimum value in the stack.
- `getMax` — Return the maximum value in the stack.

### Input Format

Each line contains a stack operation:

- `push x` — where `x` is an integer (`-10^9 <= x <= 10^9`)
- `pop`
- `peek`
- `getMin`
- `getMax`
- `exit` — to stop input and end the program

### Output Format

For every operation that returns a value (`peek`, `getMin`, `getMax`), print the result on a new line.

Other operations (`push`, `pop`) do not produce output.

### Constraints

- All operations must run in **O(1)** time and use **O(1)** additional space per operation.
- All operations are valid (no peeking or popping from an empty stack).

### Sample Test Cases

#### Input 1
```
push 2
push 2
push 1
pop
getMin
getMax
exit
```
#### Output 1
```
2
2
```

#### Input 2
```
push 3
push 1
push 6
getMin
pop
getMax
exit
```
#### Output 2
```
1
3
```
## Java Implementation

```java

import java.util.*;

class MinMaxStack{
    Stack<Integer> mainStack;
    Stack<Integer> minStack;
    Stack<Integer> maxStack;
    
    public MinMaxStack(){
        mainStack = new Stack<>();
        minStack = new Stack<>();
        maxStack = new Stack<>();
    }
    
    public void push(int data){
        mainStack.push(data);
        if(minStack.isEmpty() || minStack.peek() >= data){
            minStack.push(data);
        } else {
            minStack.push(minStack.peek());
        }
        
        if(maxStack.isEmpty() || maxStack.peek() <= data){
            maxStack.push(data);
        } else {
            maxStack.push(maxStack.peek());
        }
    }
    
    public int peek(){
        if(mainStack.isEmpty()){
            throw new RuntimeException("Stack is empty");
        }
        return mainStack.peek();
    }
    
    public int getMax(){
        if(mainStack.isEmpty()){
            throw new RuntimeException("Stack is empty");
        }
        return maxStack.peek();
    }
    
    public int getMin(){
        if(mainStack.isEmpty()){
            throw new RuntimeException("Stack is empty");
        }
        return minStack.peek();
    }
    
    public void pop(){
        if(mainStack.isEmpty()){
            System.out.println("Stack is empty");
            return;
        }
        mainStack.pop();
        minStack.pop();
        maxStack.pop();
    }
    
    
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        MinMaxStack stack = new MinMaxStack();
        while(true){
            String[] s = sc.nextLine().split("\\s+");
            try{
                switch(s[0]){
                    case "push":
                        stack.push(Integer.parseInt(s[1]));
                        break;
                    case "pop":
                        stack.pop();
                        break;
                    case "peek":
                        System.out.println(stack.peek());
                        break;
                    case "getMin":
                        System.out.println(stack.getMin());
                        break;
                    case "getMax":
                        System.out.println(stack.getMax());
                        break;
                    case "exit":
                        return;
                    default:
                        System.out.println("Invalid command");
                }
            } catch(RuntimeException e){
                System.out.println(e.getMessage());
            }
        }
    }
}
```