
[[DSA]]
[[Binary Search DSA]]

https://leetcode.com/problems/median-of-two-sorted-arrays/

one way - simply create a new array and find the median 
second way -  don't create a new array but keep on increasing the pointer until at the right position 

third way - MIND BLOWN OUT 
- basically find how many numbers are before the median first of all
- if odd then simple, if even you want to be present at the middle position
- then using shorter array, simply pick 0 to min(k, n)
- and similarly update the pointer for bigger array and find the l1, r1, l2, r2 (and create answer)
- otheriwse move left and right on the basis of clever conditions

```java
class Solution {
    public double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int n = nums1.length;
        int m = nums2.length;
        if(n > m) return findMedianSortedArrays(nums2, nums1);
        int left = (n + m)/2;
        int low = 0;
        int high = Math.min(left, n);
        while(low <= high){
            int mid = (low + high)/2;
            int rem = left - mid;
            int l1 = mid == 0 ? Integer.MIN_VALUE : nums1[mid - 1];
            int r1 = mid == n ? Integer.MAX_VALUE : nums1[mid];
            int l2 = rem == 0 ? Integer.MIN_VALUE : nums2[rem - 1]; 
            int r2 = rem == m ? Integer.MAX_VALUE : nums2[rem];
            if(l1 > r2){
                high = mid - 1;
            }else if(l2 > r1){
                low = mid + 1;
            }else{
                if((n + m) % 2 == 0){
                    return (Math.max(l1, l2) + Math.min(r1, r2))/2.0;
                }else{
                    return Math.min(r1, r2);
                }
            }
        }
        return -1;
    }
}
```