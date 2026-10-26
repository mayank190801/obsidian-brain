
[[DSA]]
[[Binary Search DSA]]

https://www.geeksforgeeks.org/problems/aggressive-cows/0

- simple binary search on answers


```java


// User function Template for Java
class Solution {
    public static int aggressiveCows(int[] stalls, int k) {
        Arrays.sort(stalls);
        int low = 0;
        int high = Integer.MAX_VALUE;
        int ans = 0;
        while(low <= high){
            int mid = low + (high - low)/2;
            if(possible(stalls, mid, k)){
                ans = mid;
                low = mid + 1;
            }else{
                high = mid - 1;
            }
        }
        return ans;
    }
    
    public static boolean possible(int[] stalls, int gap, int k){
        int placed = 0;
        int last = -1;
        for(int i = 0; i < stalls.length; i++){
            int stall = stalls[i];
            if(last == -1 || stall - last >= gap){
                placed++;
                last = stall;
            }
        }
        return placed >= k;
    }
}
```