# 📱 Problem: Phonebook Management Using Hash Tables

You're tasked with creating a **phonebook program** that supports:

✅ Storing contacts as name → number
✅ Storing reverse mapping as number → name
✅ Searching either by name or phone number
✅ Displaying results based on the query or showing a not-found message

---

### 📥 Input Format:

```
Line 1: Integer n → number of phonebook entries  
Next n lines: name and phone number separated by space  
Last line: name or phone number to search  
```

---

### 📤 Output Format:

* If search is a **name**:

  ```
  <name> is in the phonebook with number <phone_number>
  ```

* If search is a **phone number**:

  ```
  <phone_number> is associated with <name> in the phonebook
  ```

* If no match:

  ```
  No entries found for <query>
  ```

---

### 🧪 Sample Input 1:

```
3
John 9874563215
Jane 9876543210
James 9745863214
John
```

### 📌 Sample Output 1:

```
John is in the phonebook with number 9874563215
```

---

### 💻 Java Code with Comments:

```java
import java.util.*;

class PhoneBook {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        // Read number of phonebook entries
        int n = sc.nextInt();

        // Maps to store name → number and number → name
        Map<String, String> numberToName = new HashMap<>();
        Map<String, String> nameToNumber = new HashMap<>();

        // Read each entry and populate both maps
        for (int i = 0; i < n; i++) {
            String name = sc.next();
            String number = sc.next();

            numberToName.put(number, name);   // For reverse lookup
            nameToNumber.put(name, number);   // For normal lookup
        }

        // Read the search query
        String query = sc.next();

        // If the query starts with a digit, it's a number
        if (Character.isDigit(query.charAt(0))) {
            if (numberToName.containsKey(query)) {
                // Phone number found → print name
                System.out.printf("%s is associated with %s in the phonebook", query, numberToName.get(query));
            } else {
                // No such phone number
                System.out.println("No entries found for " + query);
            }
        } else {
            // Otherwise, assume it's a name
            if (nameToNumber.containsKey(query)) {
                // Name found → print phone number
                System.out.printf("%s is in the phonebook with number %s", query, nameToNumber.get(query));
            } else {
                // No such name
                System.out.println("No entries found for " + query);
            }
        }
    }
}
```

---

✅ **Note**:

* You’re using `Character.isDigit(...)` effectively to distinguish phone numbers from names.
* If needed later, you can extend this to support **case-insensitive search** or **duplicate handling**.
