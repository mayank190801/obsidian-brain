
[[Bit Manipulation DSA]]

https://leetcode.com/problems/subsets/

```java
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> ans = new ArrayList<>();
        int len = nums.length;
        int total = 1 << len;   //this is much faster implementation for fiding the power of 2 (using bits manipulation)
        for(int i = 0; i < total; i++){
            List<Integer> subset = new ArrayList<>();
            int idx = 0;
            int curr = i;
            while(curr > 0){
                if((curr & 1) == 1) subset.add(nums[idx]);
                curr = curr >> 1;
                idx++;
            }
            ans.add(subset);            
        }
        return ans;        
    }
}
```


```java
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> ans = new ArrayList<>();
        int len = nums.length;
        int total = 1 << len;
        for(int i = 0; i < total; i++){
            List<Integer> subset = new ArrayList<>();
            for(int j = 0; j < len; j++){                
                if((i & (1 << j)) > 0) subset.add(nums[j]);
            }            
            ans.add(subset);            
        }
        return ans;        
    }
}
```


