Problem Statement



Teju wants to write a program that constructs two binary trees based on user input and then checks if these trees are identical or not. 



The program takes input for the number of nodes in each tree followed by the elements of each tree in level order. It then determines whether the two trees are identical or not based on their structure and values of nodes.

Input format :
The first line of input consists of an integer n, representing the number of nodes in the first binary tree.

The second line consists of n space-separated integers, representing the elements of the first binary tree.

The third line consists of an integer m, representing the number of nodes in the second binary tree.

The fourth line consists of m space-separated integers, representing the elements of the second binary tree.

Output format :
If the two binary trees are identical, print "The given binary trees are identical".

Otherwise, print "The given binary trees are not identical".



Refer to the sample output for formatting specifications.

Code constraints :
3 ≤ n, m ≤ 30

1 ≤ tree elements ≤ 105

Sample test cases :
Input 1 :
7
1 2 3 4 5 6 7
7
1 2 3 4 5 6 7
Output 1 :
The given binary trees are identical
Input 2 :
7
1 2 3 4 5 6 7
7
1 2 3 4 5 6 8
Output 2 :
The given binary trees are not identical
Input 3 :
7
1 2 3 4 5 6 7
6
1 2 3 4 5 6
Output 3 :
The given binary trees are not identical

import java.util.*;

class Node<T>{
    T data;
    Node<T> left , right;
    public Node(T data){
        this.data = data;
        left = right = null;
    }
}

class BinaryTree<T>{
    Node<T> root;
    public BinaryTree(List<T> list){
        root = null;
        this.buildTree(list);
    }
    public void buildTree(List<T> list){
        root = new Node<>(list.remove(0));
        Queue<Node<T>> q = new LinkedList<>();
        q.offer(root);
        while(!list.isEmpty()){
            Node<T> cur = q.poll();
            cur.left = new Node(list.remove(0));
            q.offer(cur.left);
            if(!list.isEmpty()){
                cur.right = new Node(list.remove(0));
                q.offer(cur.right);
            }
        }
    }
}

class Solution{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        List<Integer> list = new ArrayList<>();
        int n = sc.nextInt();
        for(int i=0;i<n;i++){
            list.add(sc.nextInt());
        }
        BinaryTree<Integer> tree1 = new BinaryTree<>(list);
        n = sc.nextInt();
        for(int i=0;i<n;i++){
            list.add(sc.nextInt());
        }
        BinaryTree<Integer> tree2 = new BinaryTree<>(list);
        
        System.out.println(isIdentical(tree1.root , tree2.root) ? "The given binary trees are identical" : "The given binary trees are not identical");
    }
    
    private static boolean isIdentical(Node<Integer> a , Node<Integer> b){
        if(a == null && b == null) return true;
        
        if(a == null || b == null) return false;
        
        return a.data == b.data && isIdentical(a.left , b.left) && isIdentical(a.right , b.right);
    }
}