
[[DSA]]
[[Binary Search DSA]]


```java
class Solution {
    public int minDays(int[] bloomDay, int m, int k) { 
        long n = bloomDay.length;
        long total = (long)m * (long)k;
        if(total > n) return -1;
        int low = 0;
        int high = 0;
        for(int day : bloomDay) high = Math.max(high, day);
        int ans = high;
        while(low <= high){
            int mid = low + (high - low)/2;
            if(possible(bloomDay, m, k, mid)){
                ans = mid;
                high = mid - 1;   
            }else{
                low = mid + 1;
            }
        }
        return ans;        
    }

    public boolean possible(int[] bloomDay, int m, int k, int days){
        int cnt = 0;
        int adjacent = 0;
        for(int i = 0; i < bloomDay.length; i++){
            if(bloomDay[i] <= days){
                adjacent++;
                if(adjacent >= k){
                    adjacent = 0;
                    cnt++;
                }
            }else {
                adjacent = 0;
            }
        }
        return cnt >= m;
    }
}
```