# 🚀 **Task Management System Using Queue (Linked List)**

### 🧾 **Problem Statement**

Develop a basic **task management system** for a team of software developers where:

* Each **positive integer** represents a valid task ✅
* Each **negative integer** represents an erroneous task ❌

Your program must:

1. **Enqueue** all tasks
2. **Remove** erroneous tasks (negative integers)
3. **Display** the valid tasks in the order they were added

---

### 🧮 **Input Format**

```
Line 1: An integer N (number of tasks)
Line 2: N space-separated integers (task values)
```

---

### 📤 **Output Format**

For each task enqueued:

```
Enqueued: <task>
```

After filtering erroneous tasks:

```
Queue Elements after Dequeue: <valid task 1> <valid task 2> ...
```

---

### 📌 **Constraints**

* 1 ≤ N ≤ 15
* -1000 ≤ task values ≤ 1000

---

### 💻 **Java Code**

```java
import java.util.*;

public class TaskManager {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        Queue<Integer> taskQueue = new LinkedList<>();

        // Read number of tasks
        int n = sc.nextInt();

        // Enqueue tasks and print status
        for (int i = 0; i < n; i++) {
            int task = sc.nextInt();
            taskQueue.offer(task);
            System.out.println("🟢 Enqueued: " + task);
        }

        // Remove all erroneous (negative) tasks
        int size = taskQueue.size();
        for (int i = 0; i < size; i++) {
            int task = taskQueue.poll();
            if (task >= 0) {
                taskQueue.offer(task);
            }
        }

        // Print the filtered queue
        System.out.print("\n✅ Queue Elements after Dequeue: ");
        for (int task : taskQueue) {
            System.out.print(task + " ");
        }
        System.out.println(); // for clean ending
    }
}
```

---

### 🧪 **Sample Test Case 1**

**Input:**

```
5
12 -54 68 -79 53
```

**Output:**

```
🟢 Enqueued: 12
🟢 Enqueued: -54
🟢 Enqueued: 68
🟢 Enqueued: -79
🟢 Enqueued: 53

✅ Queue Elements after Dequeue: 12 68 53 
```

---

### 🧪 **Sample Test Case 2**

**Input:**

```
6
-23 -45 93 27 91 -15
```

**Output:**

```
🟢 Enqueued: -23
🟢 Enqueued: -45
🟢 Enqueued: 93
🟢 Enqueued: 27
🟢 Enqueued: 91
🟢 Enqueued: -15

✅ Queue Elements after Dequeue: 93 27 91 
```

---
