
[[DSA]]
[[Binary Search DSA]]

- nice trick of checking for odd and even indexes for next and prev element

```java
class Solution {
    public int singleNonDuplicate(int[] nums) {
        int low = 0;
        int high = nums.length - 1;
        int ans = -1;
        while (low <= high) {
            int mid = (low + high) / 2;
            int prev = mid == 0 ? Integer.MIN_VALUE : nums[mid - 1];
            int next = mid == nums.length - 1 ? Integer.MAX_VALUE : nums[mid + 1];
            if (nums[mid] != prev && nums[mid] != next)
                return nums[mid];
            if ((mid % 2 == 0 && nums[mid] == next) || (mid % 2 == 1 && nums[mid] == prev)) {
                low = mid + 1;
            } else {
                high = mid - 1;
            }
        }
        return -1;
    }
}
```