
[[Bit Manipulation DSA]]

https://leetcode.com/problems/single-number/description/


```java
class Solution {
    public int singleNumber(int[] nums) {
        int ans = 0;
        for(int num : nums){
            ans = ans ^ num;
        }
        return ans;        
    }
}
```

