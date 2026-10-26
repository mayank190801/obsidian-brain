[[DSA]]
[[Dynamic Programming DSA]]

Learning 
- Actually this is the better version for idx, buy and cap - this is only idx and trans 
- And then converting it to dp is pretty obvious 

```
   public static int maximumProfit(int[] prices, int n, int k)
    {
        int[][] dp = new int[n + 1][2*k + 1];
        for(int idx = n - 1; idx >= 0; idx--){
            for(int trans = 2*k - 1; trans >= 0; trans--){
                if(trans % 2 == 0){
                    int keepit = dp[idx + 1][trans];
                    int buyit = -prices[idx] + dp[idx + 1][trans + 1];
                    dp[idx][trans] = Math.max(keepit, buyit);
                }else{
                    int keepit = dp[idx + 1][trans];
                    int sellit = prices[idx] + dp[idx + 1][trans + 1];
                    dp[idx][trans] = Math.max(keepit, sellit);
                }
            }
        }
        return dp[0][0];
    }
```
