
[[DSA]]
[[Binary Search DSA]]

- Use long for edge cases prevention 
- Also both next and prev should min value !!!!

```java
class Solution {
    public int findPeakElement(int[] nums) {
        if(nums.length == 1) return 0;
        int low = 0;
        int high = nums.length - 1;
        while(low <= high){
            int mid = (low + high)/2;
            long prev = mid == 0 ? Long.MIN_VALUE : nums[mid - 1];
            long next = mid == nums.length - 1 ? Long.MIN_VALUE : nums[mid + 1];
            long val = nums[mid];            
            if(prev < val && val > next) return mid;
            if(prev < val && val < next){
                low = mid + 1;
            }else{
                high = mid - 1;
            }
        }
        return -1;        
    }
}
```