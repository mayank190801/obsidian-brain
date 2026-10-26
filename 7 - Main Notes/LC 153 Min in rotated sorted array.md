
[[DSA]]
[[Binary Search DSA]]

- Much simpler than last two for sure
```java
class Solution {
    public int findMin(int[] nums) {
        int low = 0;
        int high = nums.length - 1;
        int ans = Integer.MAX_VALUE;
        while(low <= high){
            int mid = (low + high)/2;
            int val = nums[mid];            
            ans = Math.min(ans, val);
            if(val < nums[high]){                
                high = mid - 1;                
            }else{
                low = mid + 1;
            }
        }
        return ans;
    }
}
```