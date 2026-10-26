[[Bit Manipulation DSA]]

https://leetcode.com/problems/single-number-iii/

- brilliant solution, using bits concept and seeing where bit is marked and where bit is not marked (logical problem solving basically)

```java
class Solution {
    public int[] singleNumber(int[] nums) {
        int xor = 0;
        for(int num : nums) xor = xor ^ num;

        xor = (xor & (xor - 1)) ^ xor;
        int seenBit = 0;
        int notSeenBit = 0;

        for(int num : nums){
            if((num & xor) != 0) seenBit = seenBit ^ num;
            else notSeenBit = notSeenBit ^ num;
        }

        return new int[]{seenBit, notSeenBit};        
    }
}
```