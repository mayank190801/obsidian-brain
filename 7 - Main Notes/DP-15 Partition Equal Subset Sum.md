[[DSA]]
[[Dynamic Programming DSA]]


https://www.naukri.com/code360/problems/partition-equal-subset-sum_892980?source=youtube&campaign=striver_dp_videos&utm_source=youtube&utm_medium=affiliate&utm_campaign=striver_dp_videos


- Same as previous one, just few more edge cases 
- Target === half of sum 

```
public static boolean canPartition(int[] arr, int n) {
        int sum = 0;
        for(int num : arr) sum += num;
        if(sum % 2 != 0) return false;
        
       
        int target = sum / 2;
        boolean[][] dp = new boolean[n][target + 1];
        for(int i = 0; i < n; i++){
            dp[i][0] = true;
        }
        if(arr[0] <= target) dp[0][arr[0]] = true;
        
        for(int i = 1; i < n; i++){
            for(int j = 1; j <= target; j++){
                boolean notTake = dp[i - 1][j];
                boolean take = false;
                if(j - arr[i] >= 0){
                    take = dp[i - 1][j - arr[i]];
                }
                dp[i][j] = take || notTake;
            }
        }
        
        return dp[n - 1][target];
    }
```

-- not much to learn from this one, just the application of the [[DP-14 Subset Sum Equals to Target]]