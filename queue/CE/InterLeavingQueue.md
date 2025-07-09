# 🧾 Problem Statement

**Gokul** is working on a program to rearrange elements in a queue. Given a queue of integers, he needs to modify it by **interleaving its first half with the second half**.

> 🔁 *Interleaving involves merging elements from two separate halves in an alternating fashion to create a new sequence.*

---

## 🔢 Input Format

* The first line of input consists of an integer `n`, representing the number of elements in the queue.
* The second line consists of `n` space-separated integers, representing the queue elements.

---

## 🖨 Output Format

* The output prints `n` space-separated integers, representing the rearranged queue after interleaving its first half with the second half.

---

## 📎 Constraints

* 2 ≤ n ≤ 10 (n will always be even)
* 1 ≤ queue elements ≤ 1000

---

## 💻 Java Code

```java
import java.util.Scanner;

class InterleavingQueue {
    private int[] queue;
    private int front;
    private int rear;
    private int size;

    public InterleavingQueue(int n) {
        queue = new int[n];
        size = n;
        front = 0;
        rear = -1;
    }

    public void enqueue(int val) {
        queue[++rear] = val;
    }

    public int dequeue() {
        if (isEmpty()) {
            throw new RuntimeException("Queue is Empty");
        }
        return queue[front++];
    }

    public boolean isEmpty() {
        return rear == -1 || front > rear;
    }

    public void interleave() {
        int half = size / 2;
        int[] first = new int[half];
        int[] second = new int[half];

        // Split into two halves
        for (int i = 0; i < half; i++) {
            first[i] = dequeue();
        }

        for (int i = 0; i < half; i++) {
            second[i] = dequeue();
        }

        // Reset queue
        front = 0;
        rear = -1;

        // Interleave
        for (int i = 0; i < half; i++) {
            enqueue(first[i]);
            enqueue(second[i]);
        }
    }

    public void printQueue() {
        for (int i = front; i <= rear; i++) {
            System.out.print(queue[i] + " ");
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();

        InterleavingQueue q = new InterleavingQueue(n);

        for (int i = 0; i < n; i++) {
            q.enqueue(sc.nextInt());
        }

        q.interleave();
        q.printQueue();
    }
}
```

---

## 🧪 Sample Test Case 1

**Input**

```
6
1 2 3 7 9 5
```

**Output**

```
1 7 2 9 3 5 
```

---

## 🧪 Sample Test Case 2

**Input**

```
4
14 62 56 41
```

**Output**

```
14 56 62 41 
```

---
