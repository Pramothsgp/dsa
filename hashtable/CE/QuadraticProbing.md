# ✈️ Problem: Senior Citizen Seat Allocation Using Quadratic Probing

---

## 🧠 Problem Statement

You are planning a trip with your family to **Goa**, and you've booked flight tickets for your family members. The air travel company uses **quadratic probing** to make seating arrangements based on **age**.

You need to write a program that:

* Stores ages using **quadratic probing** in a hash table of size 10.
* Prints the **seat numbers (indices)** of **senior citizens** (age ≥ 60).
* If no senior citizens are found, print:
  **`No senior citizens in the family`**

---

## 📥 Input Format

1. The first line contains an integer `N` – number of family members.
2. The second line contains `N` space-separated integers – ages of family members.

---

## 📤 Output Format

* For every senior citizen, output:
  **`Age: <age>, Seat: <index>`**
* If none, print:
  **`No senior citizens in the family`**

---

## 📌 Constraints

* Hash table size = 10
* 1 ≤ N ≤ 10
* 0 ≤ Age ≤ 100

---

## 🧪 Sample Test Case 1

**Input**

```
5
23 40 45 12 65
```

**Output**

```
Age: 65, Seat: 6
```

---

## 🧪 Sample Test Case 2

**Input**

```
5
23 40 45 12 25
```

**Output**

```
No senior citizens in the family
```

---

## 🧪 Sample Test Case 3

**Input**

```
6
24 26 59 60 78 81
```

**Output**

```
Age: 60, Seat: 0
Age: 81, Seat: 1
Age: 78, Seat: 8
```

---

## ✅ Java Code (Quadratic Probing - Formatted)

```java
import java.util.*;

class FlightTicket {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int size = 10;
        int[] table = new int[size];
        Arrays.fill(table, -1);

        for (int i = 0; i < n; i++) {
            int age = sc.nextInt();
            int index = age % size;
            boolean f = true;

            for (int j = 0; j < size; j++) {
                index = (index + j * j) % size;
                if (table[index] == -1) {
                    table[index] = age;
                    f = false;
                    break;
                }
            }
        }

        boolean f = true;
        for (int i = 0; i < size; i++) {
            if (table[i] >= 60) {
                System.out.printf("Age: %d, Seat: %d\n", table[i], i);
                f = false;
            }
        }

        if (f) {
            System.out.println("No senior citizens in the family");
        }
    }
}
```

---
