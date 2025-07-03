Problem Statement



Given a sorted array, write a function that creates a Balanced Binary Search Tree using array elements.



Example

Input: 

3

1 2 3



Output: 

2 1 3



Explanation:

The given input is formed like the below tree.

   2

  / \

 1  3 

A BST is considered balanced when all elements less than 2 are on the left side of 2, and all the elements greater than 2 are on the right side.

Input format :
The first line of input consists of an integer N, representing the number of elements in the sorted array.

The second line of input consists of N space-separated integers representing the elements of the sorted array.

Output format :
The output displays the preorder traversal of the constructed balanced binary search tree, separated by a space.



Refer to the sample input and output for formatting specifications.

Code constraints :
In this scenario, the given test cases will fall under the following constraints:

1 ≤ N ≤ 20

1 ≤ Elements of the array ≤ 100

Sample test cases :
Input 1 :
7
1 2 3 4 5 6 7
Output 1 :
4 2 1 3 6 5 7 
Input 2 :
3
1 2 3
Output 2 :
2 1 3 
Input 3 :
4
1 2 3 4
Output 3 :
2 1 3 4 
Input 4 :
6
50 60 70 80 90 100
Output 4 :
70 50 60 90 80 100 

import java.util.*;

class Node<T> {
    T data;
    Node<T> left , right;
    public Node(T data){
        this.data = data;
    }
}

class BST<T>{
    Node<T> root;
    public BST(){
        root = null;
    }
    
    public void buildTree(T[] data){
        root = build(data , 0 , data.length - 1);
    }
    
    private Node<T> build(T[] data , int left , int right){
        if(left > right) return null;
        int mid = left + (right - left) / 2;
        Node<T> root = new Node<>(data[mid]);
        root.left = build(data , left , mid - 1);
        root.right = build(data , mid + 1 , right);
        return root;
    }
    
    public void print(){
        preOrder(root);
    }
    
    private void preOrder(Node<T> root){
        if(root == null) return;
        System.out.print(root.data + " ");
        preOrder(root.left);
        preOrder(root.right);
    }
    
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        BST<Integer> bst = new BST<>();
        int n = sc.nextInt();
        Integer[] nums = new Integer[n];
        for(int i=0;i<n;i++){
            nums[i] = sc.nextInt();
        }
        
        bst.buildTree(nums);
        bst.print();
    }
}