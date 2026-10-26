
[[Bit Manipulation DSA]]

https://leetcode.com/problems/single-number-ii/description/


One way 
```java
class Solution {
    public int singleNumber(int[] nums) {
        int[] bits = new int[32];
        for (int num : nums) {        
            for(int idx = 0; idx < 32; idx++){
                if ((num & (1 << idx)) != 0)
                    bits[idx]++;
            }        
        }
        int ans = 0;
        for (int i = 0; i < 32; i++) {
            if (bits[i] % 3 == 1)
                ans += (1 << i);
        }        
        return ans;
    }
}
```

- Go through all 32 bits, (to handle negative number cases as well)

Second way
Using seenOnce and seenTwice (will get deeper into it later on)