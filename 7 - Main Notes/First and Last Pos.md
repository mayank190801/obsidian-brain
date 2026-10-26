
[[Binary Search DSA]]
[[DSA]]

https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/description/


```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        return new int[] {indexFinder(nums, target, true), indexFinder(nums, target, false)};        
    }

    public int indexFinder(int[] nums, int target, boolean lower){
        int low = 0;
        int high = nums.length - 1;
        int ans = -1;
        while(low <= high){
            int mid = (low + high)/2;
            if(nums[mid] == target){
                ans = mid;
                if(lower) high = mid - 1;
                else low = mid + 1; 
            }else if(nums[mid] < target){
                low = mid + 1;
            }else{
                high = mid - 1;
            }
        }
        return ans;
    }
}
```


