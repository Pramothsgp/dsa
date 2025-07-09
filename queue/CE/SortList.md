# 🚌 Sorting Bus Ticket Request Timestamps Using LinkedList in Java

This program is designed for a **bus ticketing system**, where each request comes with a **timestamp**. To process the requests in the correct order, we need to **sort the timestamps in ascending order**.

---

## 📌 Problem Statement

* **Input**:

  * First line: An integer `n` — the number of ticket requests.
  * Second line: `n` space-separated integers representing timestamps.
* **Output**:

  * A single line containing the **sorted** timestamps, space-separated.

---

## 📎 Sample Input & Output

### ✅ Input

```
5
10 26 29 28 17
```

### ✅ Output

```
10 17 26 28 29
```

---

## ✅ Java Implementation

```java
import java.util.*;

class SortList {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // Read the number of ticket requests
        int n = sc.nextInt();

        // Create a LinkedList to store timestamps
        LinkedList<Integer> list = new LinkedList<>();

        // Read each timestamp into the list
        for (int i = 0; i < n; i++) {
            list.add(sc.nextInt());
        }

        // Sort the LinkedList using Collections utility
        Collections.sort(list);

        // Print the sorted list without brackets or commas
        System.out.println(list.toString().replaceAll("\\[|\\]|,", ""));
    }
}
```

---

## 🧠 Key Notes

* **Data Structure Used**: `LinkedList<Integer>`
* **Sorting Utility**: `Collections.sort()` (uses TimSort – efficient for small `n`)
* **Regex Cleanup**: Replaces square brackets and commas to meet output format

---

## 💡 Optional Enhancement

If you want to **sort without using `Collections.sort()`**, you can try recursion-based or manual sorting (e.g., selection sort on linked lists), but this is optimal for production use.

---