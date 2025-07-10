# 🧮 Problem: Top K Students Using Hash Table

You're a teacher who wants to **reward the top-performing students** in your class based on their marks. You’re given the names and marks of `N` students and need to identify the **top K students**.

To do this:

* Store the names and marks in a list of student objects.
* Sort them based on marks in descending order.
* Display the top `K` students.

---

### 📥 Input Format

```
Line 1: Integer N → Total number of students
Line 2: Integer K → Number of top students to display
Next N lines: Each contains a student's name followed by their mark
```

---

### 📤 Output Format

```
K lines, each in the format:
<name> : <mark>
(From highest to lowest mark)
```

---

### ✅ Constraints

* 1 ≤ N ≤ 10
* 1 ≤ K ≤ N

---

### 🔎 Sample Input 1

```
5
3
John 90
Alice 80
Bob 85
Sarah 95
Mike 75
```

### ✅ Sample Output 1

```
Sarah : 95
John : 90
Bob : 85
```

---

### 🔎 Sample Input 2

```
3
1
Alice 100
Bob 64
Charles 79
```

### ✅ Sample Output 2

```
Alice : 100
```

---

### 🧠 Explanation

* In Sample 1, the top 3 students based on marks are Sarah, John, and Bob.
* In Sample 2, Alice is the only top scorer requested.

---

### 💻 Java Code (unchanged):

```java
import java.util.*;

class Student{
    String name;
    int mark;
    public Student(String n , int m){
        name = n;
        mark = m;
    }
    
    @Override
    public String toString(){
        return name + " : " + mark;
    }
}

class HashTable{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int k = sc.nextInt();
        List<Student> list = new ArrayList<>();
        for(int i=0;i<n;i++){
            list.add(new Student(sc.next() , sc.nextInt()));
        }
        Collections.sort(list , (a , b) -> Integer.compare(b.mark , a.mark));
        for(int i=0;i<k;i++){
            System.out.println(list.get(i));
        }
    }
}
```

---
