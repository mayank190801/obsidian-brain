
[[DSA]]
[[Greedy DSA]]

- pretty cool 
- so l and r range you create 
- with one jump, what is the next l and r range that could be created , that is the best we can do with 2 jumps? and so on 
- update l and r and increase the jump count 

```java
class Solution {
    public int jump(int[] nums) {
        int cnt = 0;
        int l = 0;
        int r = 0;
        int n = nums.length;
        if(n == 1) return 0;
        while(true){
            int nextBest = r;
            for(int idx = l; idx <= r; idx++){
                nextBest = Math.max(nextBest, nums[idx] + idx);
            }
            if(nextBest >= n - 1) return cnt + 1;            
            cnt++;
            l = r + 1;
            r = nextBest;
        }
    }
}
```