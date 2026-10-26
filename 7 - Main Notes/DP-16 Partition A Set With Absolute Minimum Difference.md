[[DSA]]
[[Dynamic Programming DSA]]

https://www.naukri.com/code360/problems/partition-a-set-into-two-subsets-such-that-the-difference-of-subset-sums-is-minimum_842494?source=youtube&campaign=striver_dp_videos&utm_source=youtube&utm_medium=affiliate&utm_campaign=striver_dp_videos


```
 public static int minSubsetSumDifference(int []arr, int n) {
        int sum = 0;
        for(int num : arr) sum += num;

        boolean[][] dp = new boolean[n][sum + 1];
        for(int i = 0; i < n; i++){
            dp[i][0] = true;
        }
        dp[0][arr[0]] = true;
        
        for(int i = 1; i < n; i++){
            for(int j = 1; j <= sum; j++){
                boolean notTake = dp[i - 1][j];
                boolean take = false;
                if(j - arr[i] >= 0){
                    take = dp[i - 1][j - arr[i]];
                }
                dp[i][j] = take || notTake;
            }
        }
        
        int ans = sum;
        for(int i = 0; i <= sum; i++){
            if(dp[n - 1][i]){
                ans = Math.min(ans, Math.abs(sum - 2*i));
            }
        }
        return ans;
    }
```

- Using [[DP-14 Subset Sum Equals to Target]] core logic only 
- Now once we know what all possible subset could be possible with the given array 
- We just use that tabulation database for our advantage, simple as that 
- How would the recursive solution look like for this bad boy?? (think about it)