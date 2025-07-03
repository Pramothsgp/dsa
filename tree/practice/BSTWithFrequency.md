# 🌳 BST With Frequency

Rao wants to analyze the frequency of words in a collection of text. He plans to implement a program using a **Binary Search Tree (BST)** to efficiently store and manage the words along with their frequencies.

---

## 📋 Problem Requirements

- **Input:**  
    - A series of words separated by spaces.  
    - Each word contains only alphabetical characters (max length: 99).
    - Input ends when the word `"end"` is entered.

- **Output:**  
    - All unique words in alphabetical order, with their frequencies.
    - The most frequent word and its frequency.

---

## 📥 Input Format

```txt
word1 word2 word3 ... end
```

---

## 📤 Output Format

```txt
Words in alphabetical order:
word1 (n times)
word2 (n times)
...
wordN (n times)
The most frequent word: [word] (n times)
```

---

## 🧪 Sample Test Cases

<details>
<summary><strong>Input 1</strong></summary>

```txt
apple banana cherry cherry apple apple
end
```

**Output 1**
```txt
Words in alphabetical order:
apple (3 times)
banana (1 times)
cherry (2 times)
The most frequent word: apple (3 times)
```
</details>

<details>
<summary><strong>Input 2</strong></summary>

```txt
programming code debugging programming testing
end
```

**Output 2**
```txt
Words in alphabetical order:
code (1 times)
debugging (1 times)
programming (2 times)
testing (1 times)
The most frequent word: programming (2 times)
```
</details>

---

## 🚦 Constraints

- The length of each word is ≤ 99 characters.

---

## 💻 Java Implementation

```java
import java.util.*;

// Node class representing each word and its frequency in the BST
class Node<T> {
        T data;           // The word
        int freq;         // Frequency of the word
        Node<T> left, right; // Left and right children

        // Constructor to initialize node with data
        public Node(T data) {
                this.data = data;
                this.freq = 1;
                left = right = null;
        }

        // Increment the frequency count
        public void inc() {
                this.freq++;
        }
}

// BST class for storing words and their frequencies
class BST<T extends Comparable<T>> {
        Node<T> root; // Root of the BST
        Node<T> res;  // Node with the highest frequency

        // Constructor to initialize BST
        public BST() {
                root = null;
                res = null;
        }

        // Public method to insert data into the BST
        public void insert(T data) {
                root = insert(root, data);
        }

        // Helper method to insert data recursively
        private Node<T> insert(Node<T> root, T data) {
                if (root == null) {
                        return new Node<>(data);
                }

                if (root.data.equals(data)) {
                        root.inc(); // Increment frequency if word already exists
                } else if (root.data.compareTo(data) > 0) {
                        root.left = insert(root.left, data); // Insert in left subtree
                } else {
                        root.right = insert(root.right, data); // Insert in right subtree
                }
                return root;
        }

        // Print words in alphabetical order and return the most frequent node
        public Node<T> print() {
                inOrder(root);
                return res;
        }

        // In-order traversal to print words and find the most frequent word
        private void inOrder(Node<T> root) {
                if (root == null) return;
                inOrder(root.left);
                System.out.print(root.data);
                System.out.printf(" (%d times)\n", root.freq);
                if (res == null || res.freq < root.freq) {
                        res = root; // Update most frequent word
                }
                inOrder(root.right);
        }

        // Main method to read input, build BST, and print results
        public static void main(String[] args) {
                Scanner sc = new Scanner(System.in);
                BST<String> bst = new BST<>();
                String s;
                // Read words until "end" is encountered
                while (!(s = sc.next()).equals("end")) {
                        bst.insert(s);
                }
                System.out.println("Words in alphabetical order:");
                Node<String> res = bst.print();
                System.out.printf("The most frequent word: %s (%d times)", res.data, res.freq);
        }
}
```

---

> **Tip:**  
> You can adapt this approach for other data types or frequency analysis problems by modifying the node structure and comparison logic.

