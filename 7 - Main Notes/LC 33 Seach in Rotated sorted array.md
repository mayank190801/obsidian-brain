

[[DSA]]
[[Binary Search DSA]]

```java
class Solution {
    public int search(int[] nums, int target) {
        int low = 0;
        int high = nums.length - 1;
        while(low <= high){
            int mid = (low + high)/2;
            int val = nums[mid];
            if(val == target) return mid;
            if(val >= nums[low]){
                if(target < val && target >= nums[low]){
                    high = mid - 1;
                }else {
                    low = mid + 1;
                }
            }else{
                if(target > val && target <= nums[high]) {
                    low = mid + 1;
                }else {
                    high = mid - 1;
                }
            }
        }

        return -1;        
    }
}
```