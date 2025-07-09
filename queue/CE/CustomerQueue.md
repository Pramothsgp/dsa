## 🧾 Problem Statement

Imagine a bustling coffee shop where customers are placing their orders for their favorite coffee drinks. The cafe owner, **Sheeren**, wants to efficiently manage the queue of coffee orders using a digital system. You are tasked with creating a program to handle this **queue of orders**.

Each character in the queue represents a customer's coffee order:

* `'L'` → Latte
* `'E'` → Espresso
* `'M'` → Macchiato
* `'O'` → Iced Coffee
* `'N'` → Nabob

The system should support the following operations:

---

## 🔢 Input Format

* The input consists of **menu-driven choices**:

  1. **Enqueue** a coffee order
     → Next line will have one character `'L'`, `'E'`, `'M'`, `'O'`, or `'N'`
  2. **Dequeue** the first coffee order
  3. **Display** all orders in the queue
  4. **Exit** the program

---

## 🖨 Output Format

* Based on the user's choice:

  * Enqueue:

    ```
    Order for X is enqueued.
    ```

    or

    ```
    Queue is full. Cannot enqueue more orders.
    ```

  * Dequeue:

    ```
    Dequeued Order: X
    ```

    or

    ```
    No orders in the queue.
    ```

  * Display:

    ```
    Orders in the queue are: X Y Z ...
    ```

    or

    ```
    Queue is empty. No orders available.
    ```

  * Exit:

    ```
    Exiting program
    ```

  * Invalid:

    ```
    Invalid option.
    ```

---

## 📎 Constraints

* Maximum queue size = **5**
* Allowed coffee order characters: `'L'`, `'E'`, `'M'`, `'O'`, `'N'`

---

## 💻 Java Code Implementation

```java
import java.util.Scanner;

class OrderQueue {
    private final int SIZE = 5;
    private char[] orders = new char[SIZE];
    private int front = -1;
    private int rear = -1;

    public void initializeQueue() {
        front = 0;
    }

    public boolean isEmpty() {
        return rear == -1 || rear < front;
    }

    public boolean isFull() {
        return rear >= SIZE - 1;
    }

    public boolean enqueue(char order) {
        if (isFull()) {
            System.out.println("Queue is full. Cannot enqueue more orders.");
            return false;
        }

        if (rear == -1) {
            front = 0;
        }

        orders[++rear] = order;
        System.out.printf("Order for %c is enqueued.%n", order);
        return true;
    }

    public boolean dequeue(char[] order) {
        if (isEmpty()) {
            return false;
        }

        order[0] = orders[front++];

        // Reset queue if it becomes empty
        if (front > rear) {
            front = 0;
            rear = -1;
        }

        return true;
    }

    public void display() {
        if (isEmpty()) {
            System.out.println("Queue is empty. No orders available.");
            return;
        }

        System.out.print("Orders in the queue are: ");
        for (int i = front; i <= rear; i++) {
            System.out.print(orders[i] + " ");
        }
        System.out.println();
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        OrderQueue queue = new OrderQueue();
        queue.initializeQueue();

        while (true) {
            if (!scanner.hasNextInt()) {
                break;
            }

            int choice = scanner.nextInt();

            switch (choice) {
                case 1:
                    if (scanner.hasNext()) {
                        char order = scanner.next().charAt(0);
                        queue.enqueue(order);
                    }
                    break;

                case 2:
                    char[] dequeuedOrder = new char[1];
                    if (queue.dequeue(dequeuedOrder)) {
                        System.out.println("Dequeued Order: " + dequeuedOrder[0]);
                    } else {
                        System.out.println("No orders in the queue.");
                    }
                    break;

                case 3:
                    queue.display();
                    break;

                case 4:
                    System.out.println("Exiting program");
                    return;

                default:
                    System.out.println("Invalid option.");
                    break;
            }
        }

        scanner.close();
    }
}
```

---

## 🧪 Sample Test Case 1

```
Input:
1
L
1
E
1
M
1
O
1
N
1
O
3
2
3
4

Output:
Order for L is enqueued.
Order for E is enqueued.
Order for M is enqueued.
Order for O is enqueued.
Order for N is enqueued.
Queue is full. Cannot enqueue more orders.
Orders in the queue are: L E M O N
Dequeued Order: L
Orders in the queue are: E M O N
Exiting program
```

---

## 🧪 Sample Test Case 2

```
Input:
2
3
4

Output:
No orders in the queue.
Queue is empty. No orders available.
Exiting program
```

