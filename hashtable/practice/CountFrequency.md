Single File Programming Question
Problem Statement



Suppose you are a teacher, and you have a list of words spoken by your students during a class discussion. You want to count how many times each word has been mentioned while preserving the original order. 



To do this, you decide to use a Hashtable to store the words as keys and their respective frequencies as values. This will help you identify the most commonly used words and facilitate discussions on related topics in future classes.



You are given a list of N words or numbers, count the frequency of each word in the list while preserving the original order.

Input format :
The input consists of a space-separated list of strings or integers.

Output format :
The output prints the frequency of the given list by preserving the original order.



Refer to the sample output for formatting specifications.

Code constraints :
The given test cases fall under the following specifications:

1 ≤ length of each word ≤ 100

Sample test cases :
Input 1 :
cat dog cat bird bird bird
Output 1 :
cat : 2
dog : 1
bird : 3
Input 2 :
1 2 1 2 3 6 5 6
Output 2 :
1 : 2
2 : 2
3 : 1
6 : 2
5 : 1

import java.util.*;

class CountFrequency{
    public static void main(String[] args){
        Scanner sc = new Scanner(System.in);
        Map<String , Integer> freq = new HashMap<>();
        String[] str = sc.nextLine().split("\\s+");
        for(String s : str){
            freq.put(s , freq.getOrDefault(s , 0) + 1);
        }
        Set<String> set = new HashSet<>();
        for(String s : str){
            if(!set.contains(s)){
                System.out.printf("%s : %d\n" , s , freq.get(s));
                set.add(s);
            }
        }
    }
}
