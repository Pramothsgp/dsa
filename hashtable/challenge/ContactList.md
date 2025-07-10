# 💼 **Problem: Contact List Manager with Hashing**

In a messaging application, users maintain a contact list with names and corresponding phone numbers.
Your task is to build a **Contact List Manager** using a **dictionary (hash map)** that allows:

* ✅ Adding contacts
* ❌ Deleting a specific contact
* 🔍 Checking if a contact exists
* 📃 Printing the contact list in **order of insertion**

---

### 📥 **Input Format**

* First line: An integer `n` representing the number of contacts.
* Next `n` lines: Each line contains two strings — `Name` and `PhoneNumber`.
* Last line: A string `k` representing the contact name to be **removed**.

---

### 📤 **Output Format**

* If the contact exists:

  * Line 1: `"The given key is removed!"`
  * Next `n-1` lines: Print all remaining contacts in the format:
    `Key: <Name>; Value: <PhoneNumber>`

* If the contact **does not exist**:

  * Line 1: `"The given key is not found!"`
  * Next `n` lines: Print all contacts unchanged.

---

### 🔐 **Constraints**

* 2 ≤ n ≤ 50
* Contact names are **case-sensitive**
* 3 ≤ Length of input strings ≤ 10

---

### 🧪 **Sample Test Case 1**

**Input:**

```
3
Alice 1234567890
Bob 9876543210
Charlie 4567890123
Bob
```

**Output:**

```
The given key is removed!
Key: Alice; Value: 1234567890
Key: Charlie; Value: 4567890123
```

---

### 🧪 **Sample Test Case 2**

**Input:**

```
2
Quinn 1112223333
Roger 2223334444
Sarah
```

**Output:**

```
The given key is not found!
Key: Quinn; Value: 1112223333
Key: Roger; Value: 2223334444
```

---

### ✅ **Java Code Implementation**

```java
import java.util.*;

class ContactList {
    private HashMap<String, String> contacts;
    private LinkedList<String> insertionOrder;

    public ContactList() {
        contacts = new HashMap<>();
        insertionOrder = new LinkedList<>();
    }

    // Method to insert n contacts
    private void insertContacts(Scanner sc) {
        int n = sc.nextInt();
        sc.nextLine(); // Consume leftover newline

        for (int i = 0; i < n; i++) {
            String[] parts = sc.nextLine().split("\\s+");
            String name = parts[0];
            String number = parts[1];

            contacts.put(name, number);
            insertionOrder.add(name);
        }
    }

    // Method to remove a contact
    private void removeContact(String key) {
        if (!contacts.containsKey(key)) {
            System.out.println("The given key is not found!");
        } else {
            contacts.remove(key);
            insertionOrder.remove(key);
            System.out.println("The given key is removed!");
        }
    }

    // Method to print all contacts in insertion order
    private void printContacts() {
        for (String name : insertionOrder) {
            System.out.printf("Key: %s; Value: %s\n", name, contacts.get(name));
        }
    }

    // Main driver method
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        ContactList contactList = new ContactList();

        contactList.insertContacts(sc);
        String keyToRemove = sc.nextLine();

        contactList.removeContact(keyToRemove);
        contactList.printContacts();

        sc.close();
    }
}
```

---
