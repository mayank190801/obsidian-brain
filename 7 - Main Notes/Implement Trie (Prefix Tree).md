
[[Trie DSA]]

https://leetcode.com/problems/implement-trie-prefix-tree/description/

```java

public class Trie {


    //Initialize your data structure here
    private static Node root;

    Trie() {
        root = new Node();
    }


    //Inserts a word into the trie

    public static void insert(String word) {
        Node node = root;
        for(char ch : word.toCharArray()){
            if(node.get(ch) == null){
                node.put(ch, new Node());                
            }
            node = node.get(ch);
        }
        node.setEnd();        
    }


    //Returns if the word is in the trie
    public static boolean search(String word) {
        Node node = root;
        for(char ch : word.toCharArray()){
            if(node.get(ch) == null) return false;
            node = node.get(ch);
        }
        return node.getEnd();
    }

    
    //Returns if there is any word in the trie that starts with the given prefix

    public static boolean startsWith(String prefix) {
        Node node = root;
        for(char ch : prefix.toCharArray()){
            if(node.get(ch) == null) return false;
            node = node.get(ch);
        }
        return true;
    }

    public static class Node {
    Node[] links; 
    boolean isEnd;

    public Node() {
        this.links = new Node[26];
        this.isEnd = false;
    }

    public boolean containsKey(char ch){
        return links[ch - 'a'] != null;
    }

    public void put(char ch, Node node){
        links[ch - 'a'] = node;
    }

    public Node get(char ch){
        return links[ch - 'a'];
    }

    public void setEnd(){
        this.isEnd = true;
    }

    public boolean getEnd(){
        return this.isEnd;
    }
}
}
```