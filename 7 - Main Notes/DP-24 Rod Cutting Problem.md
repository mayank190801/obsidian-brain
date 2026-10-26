[[DSA]]
[[Dynamic Programming DSA]]

[Rod cutting problem - Naukri Code 360](https://www.naukri.com/code360/problems/rod-cutting-problem_800284?source=youtube&campaign=striver_dp_videos&utm_source=youtube&utm_medium=affiliate&utm_campaign=striver_dp_videos&leftPanelTabValue=SUBMISSION)


```
    public static int cutRod(int[] price, int n){
        int[] dp = new int[n + 1];
        dp[1] = price[0];
        for(int i = 2; i <= n; i++){
            int best = 0;
            for(int j = 1; j <= i; j++){
                int curr = price[j] + dp[i - j];
                best = Math.max(best, curr);
            }
        }
        return dp[n];
    }
```

You can solve this question with normal recursion fashion, that keep cutting from 1 to n, and ask for the rest to bring the best cutout for the rod

**Striver sovled with the below ideaology** 
OR You can solve it like knapsack, that we have N length max, and I have 5 objects with different lengths and their best price to sell for (it eventually would have been under 1D dp only if you think about it - hence pretty cool problem )