
[[DSA]]
[[Binary Search DSA]]

https://www.naukri.com/code360/problems/k-th-element-of-2-sorted-array_1164159?leftPanelTabValue=PROBLEM

- similar to finding the median in sorted array
- but edge case being that low = max(k - m , 0); (really important)
```java
import java.util.ArrayList;
class Solution {
    public static int kthElement(ArrayList<Integer> arr1, ArrayList<Integer> arr2, int n, int m, int k) {            
        if(n > m) return kthElement(arr2, arr1, m, n, k);
        int left = k;
        int low = Math.max(k - m, 0);
        int high = Math.min(left, n);
        while(low <= high){
            int mid = (low + high)/2;
            int rem = left - mid;
            int l1 = mid <= 0 ? Integer.MIN_VALUE : arr1.get(mid - 1);
            int r1 = mid >= n ? Integer.MAX_VALUE : arr1.get(mid);
            int l2 = rem <= 0 ? Integer.MIN_VALUE : arr2.get(rem - 1);
            int r2 = rem >= m ? Integer.MAX_VALUE : arr2.get(rem);
            if(l1 > r2){
                high = mid - 1;
            }else if(l2 > r1){
                low = mid + 1;
            }else{
                return Math.max(l1, l2);
            }
        }
        return -1;
    }
}
```