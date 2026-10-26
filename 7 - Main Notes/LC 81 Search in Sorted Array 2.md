

[[DSA]]
[[Binary Search DSA]]


Best part about this question 
	- uses similar concepts as previous one 
	- and in case of an edge condition simply reduce the search space (pretty smart)

```java
class Solution {
    public boolean search(int[] nums, int target) {
        int low = 0;
        int high = nums.length - 1;
        while(low <= high){
            int mid = (low + high)/2;
            int val = nums[mid];
            if(val == target) return true;
            if(val == nums[low] && val == nums[high]){
                low = low + 1;
                high = high - 1;
            }else if(val >= nums[low]){
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

        return false;        
    }
}
```