
[[Trie DSA]]

https://leetcode.com/problems/implement-trie-ii-prefix-tree/description/

```java
import java.util.* ;
import java.io.*; 
public class Trie {

    public Node root;

    public Trie() {
        root = new Node();  //this does make some sense no? 
    }

    public void insert(String word) {
        Node node = root;
        for(char ch : word.toCharArray()){
            if(!node.containsKey(ch)){
                node.set(ch, new Node());
            }
            node.count[ch - 'a']++;
            node = node.get(ch);
        }
        node.end++;
    }

    public int countWordsEqualTo(String word) {
        Node node = root;
         for(char ch : word.toCharArray()){
            if(!node.containsKey(ch)) return 0;            
            node = node.get(ch);
        }
        return node.end;
    }

    public int countWordsStartingWith(String word) {
         Node node = root;
         int min = Integer.MAX_VALUE;
         for(char ch : word.toCharArray()){
            if(!node.containsKey(ch)) return 0;            
            min = Math.min(min, node.count[ch - 'a']);
            node = node.get(ch);
        }
        return min;
    }

    public void erase(String word) {
        Node node = root;
        for(char ch : word.toCharArray()){            
            node.count[ch - 'a']--;
            node = node.get(ch);
        }
        node.end--;
    }

    public class Node {
        Node[] links;
        int[] count;        
        int end;

        Node(){
            links = new Node[26];
            count = new int[26];
            end = 0;            
        }

        // 5 functions at all time brotherr
        public boolean containsKey(char ch){
            return links[ch - 'a'] != null;
        }

        public Node get(char ch){
            return links[ch - 'a'];
        }

        public void set(char ch, Node node){
            links[ch - 'a'] = node;
        }

    }
}


```