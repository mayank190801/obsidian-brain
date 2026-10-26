
[[DSA]]
[[Binary Search DSA]]

https://leetcode.com/problems/kth-missing-positive-number/


- Intuition? 
- If at some index, and if idx + K < val (then that would be the answer!!)
- Otherwise move a bit forward brother 
- Also handle edge cases nicely

First way 
```java
class Solution {
    public int findKthPositive(int[] arr, int k) {
        for(int i = 0; i < arr.length; i++){
            if(arr[i] <= k) k++;
            else break;
        }
        return k;
    }
}
```

Second way 
```java
class Solution {    
    public int findKthPositive(int[] arr, int k) {
        int low = 0;
        int high = arr.length;
        int ans = -1;
        while(low <= high){
            int mid = (low + high)/2;
            int val = mid == arr.length ? Integer.MAX_VALUE - 10000 : arr[mid];
            if(k + mid < val){
                ans = k + mid;
                high = mid - 1;
            }else{
                low = mid + 1;
            }
        }
        return ans;
    }
}
```