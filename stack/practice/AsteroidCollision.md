# 🚀 Asteroid Collision Problem

You're given an **array of integers** called `asteroids`. Each integer represents an asteroid's **size and direction**:

- **Positive value**: Asteroid moves **right**.
- **Negative value**: Asteroid moves **left**.
- All asteroids move at the **same speed**.

> **Note:**  
> Asteroids moving in the same direction will **never collide**.

When a **right-moving** asteroid meets a **left-moving** asteroid, a collision may occur:

- The **smaller** asteroid (by absolute value) **explodes**.
- If both are the **same size**, **both explode**.
- The **larger** one (by absolute value) **survives**.

---

## 📝 Your Task

Write a function that takes the `asteroids` array as input and returns a **new array** representing the state of the asteroids **after all possible collisions**.

---

## 📥 Input Format

- A single line of **space-separated integers** representing asteroid sizes and directions.

## 📤 Output Format

- A single line of **space-separated integers** representing the asteroids that remain after all collisions.

> _Refer to the sample output for formatting._

---

## 🔒 Constraints

- `1 ≤ asteroids.length ≤ 10⁴`
- Each `asteroids[i]` is a **non-zero integer** in the range `[-1000, 1000]`
- No two asteroids occupy the same position initially.

---

## 💡 Sample Test Cases

### Input 1
```
5 10 -5
```
**Output 1**
```
5 10
```

---

### Input 2
```
10 2 -2
```
**Output 2**
```
10
```

---

## 💻 Example Solution (Java)

```java
import java.util.*;

class AsteroidCollision {
    public static void main(String[] args) {
        // Read input as a line of space-separated integers
        String[] s = new Scanner(System.in).nextLine().trim().split(" ");
        int[] asteroids = new int[s.length];
        for (int i = 0; i < asteroids.length; i++) {
            asteroids[i] = Integer.parseInt(s[i]);
        }

        // Compute the result after all collisions
        List<Integer> res = asteroidCollision(asteroids);
        for (int num : res) {
            System.out.printf("%d ", num);
        }
    }

    // Function to simulate asteroid collisions
    private static List<Integer> asteroidCollision(int[] asteroids) {
        Stack<Integer> stack = new Stack<>();
        for (int a : asteroids) {
            boolean alive = true;
            // Check for collision: right-moving asteroid meets left-moving asteroid
            while (alive && a < 0 && !stack.isEmpty() && stack.peek() > 0) {
                int top = stack.peek();
                if (top < -a) {
                    // Top asteroid explodes, continue checking
                    stack.pop();
                } else if (top == -a) {
                    // Both asteroids explode
                    stack.pop();
                    alive = false;
                } else {
                    // Current asteroid explodes
                    alive = false;
                }
            }
            if (alive) {
                // Asteroid survives, add to stack
                stack.push(a);
            }
        }

        // Return the remaining asteroids as a list
        return new ArrayList<>(stack);
    }
}
```