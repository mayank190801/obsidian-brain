

[[Trie DSA]]


https://leetcode.com/problems/number-of-distinct-substrings-in-a-string/description/


Really dope ass question 
- Can be solved using O(N^2 * logN) (using hashmap simply)
- Can be solved using hashing the string (string hashing algorithm)
- Can be solved using trie, and storing the strings in a trie data structure for saving space!!! 

```java
class Solution {

    public class Node {
        Node[] links;
        boolean isEnd;

        Node() {
            links = new Node[26];
            isEnd = false;
        }

        public boolean contains(char ch) {
            return links[ch - 'a'] != null;
        }

        public Node get(char ch) {
            return links[ch - 'a'];
        }

        public void set(char ch, Node node) {
            links[ch - 'a'] = node;
        }
    }

    //woah, crazy O(N^2) solution 
    //crazy crazy crazy, insane optimisations are possible if you know trie well brother
    //that waas amazing!!! 
    //let's figure out O(Nlogn and O(N)) and get more deeper into string matching and stuff
    //hashing algoirhtms abnd what no
    public int countDistinct(String s) {
        Node root = new Node();
        int len = s.length();
        int cnt = 0;
        char[] sArr = s.toCharArray();
        for (int i = 0; i < len; i++) {
            Node curr = root;
            for (int j = i; j < len; j++) {
                if (!curr.contains(sArr[j])) {
                    curr.set(sArr[j], new Node());
                    cnt++;
                }
                curr = curr.get(sArr[j]);
            }
        }
        return cnt;
    }

}
```