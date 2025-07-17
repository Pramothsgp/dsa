Here's your **single-file Python solution** to the **Merge k Sorted Lists** problem, formatted with:

* ✅ Problem Statement
* 📥 Input / 📤 Output Format
* 🧪 Sample Test Cases
* 🧠 Explanation
* 💻 Clean Python Code (using sorting)
* ⏱ Time and Space Complexity

---

# 🔗 Merge k Sorted Lists

---

## 📝 Problem Statement

You're given an array of `k` linked lists. Each linked list is **sorted in ascending order**.

Your task is to **merge all the linked lists into one sorted list**, and **print the values in order**.

---

## 📥 Input Format

* First line: Integer `k`, number of linked lists
* For each of the `k` linked lists:

  * Line 1: Integer `n`, number of elements in the list
  * Line 2: `n` space-separated integers in ascending order

## 📤 Output Format

* Print the merged sorted list, elements separated by a space

---

## 🧪 Sample Test Cases

### Input 1:

```
3
3
1 4 5
3
1 3 4
2
2 6
```

### Output 1:

```
1 1 2 3 4 4 5 6 
```

---

### Input 2:

```
2
2
1 5
3
2 6 7
```

### Output 2:

```
1 2 5 6 7 
```

---

## 💡 Explanation

We flatten all `k` sorted lists into one big list, sort it, and print the result.

This works efficiently because the total number of elements is ≤ 10⁴.

---

## ✅ Python Code (Using Sorting)

```python
n = int(input())
l = []

for _ in range(n):
    size = int(input())
    if size > 0:
        nums = list(map(int, input().split()))
        l.extend(nums)
    else:
        # read the empty line if list size is 0
        input()

l.sort()

for i in l:
    print(i, end=' ')
```

---

## ⏱ Time and Space Complexity

| Metric           | Value      |
| ---------------- | ---------- |
| Time Complexity  | O(N log N) |
| Space Complexity | O(N)       |

Where `N` is the total number of elements across all linked lists.

---

> ✅ This is a simple and efficient approach within given constraints. For optimal O(N log k) solution, a **min-heap** can be used with actual LinkedList node objects.
