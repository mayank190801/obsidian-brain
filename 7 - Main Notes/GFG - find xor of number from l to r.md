
[[Bit Manipulation DSA]]

https://www.geeksforgeeks.org/problems/find-xor-of-numbers-from-l-to-r/1?itm_source=geeksforgeeks&itm_medium=article&itm_campaign=practice_card

- Tc - O(1)
- Sc - O(1)

```java
class Solution {
    public static int findXOR(int l, int r) {
        return findXORofN(r) ^ findXORofN(l - 1);
    }
    
    public static int findXORofN(int n){
        if(n % 4 == 0){
            return n;
        }
        if(n % 4 == 1){
            return 1;
        }
        if(n % 4 == 2){
            return n + 1;
        }
        return 0;
    }
}
```