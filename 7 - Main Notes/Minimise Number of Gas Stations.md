
[[DSA]]
[[Binary Search DSA]]

Leetcode premium!
https://leetcode.com/problems/minimize-max-distance-to-gas-station/description/

```java
class Solution {
    public double minmaxGasDist(int[] stations, int k) {        
        double low = 0.0;
        double high = 1e8;    
        double ans = -1;     
        while(high - low > 1e-6){
            double mid = low + (high - low)/2.0;            
            if(possible(stations, k, mid)){
                ans = mid;
                high = mid;
            }else{
                low = mid;
            }            
        }
        return ans;        
    }

    public boolean possible(int[] stations, int k, double penalty){
        int require = 0;      
        for(int i = 1; i < stations.length; i++){            
            require += (int)((stations[i] - stations[i - 1])/penalty);
        }
        return require <= k;
    }
}
```