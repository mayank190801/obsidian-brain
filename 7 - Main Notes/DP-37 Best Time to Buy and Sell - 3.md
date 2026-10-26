[[DSA]]
[[Dynamic Programming DSA]]

[Best Time to Buy and Sell Stock III - Naukri Code 360](https://www.naukri.com/code360/problems/buy-and-sell-stock_1071012?source=youtube&campaign=striver_dp_videos&utm_source=youtube&utm_medium=affiliate&utm_campaign=striver_dp_videos&leftPanelTabValue=SUBMISSION)

Learnings and improvement afterwards 
- You can convert this question to 2D array (optimise the space and stuff)
- Take motivation for buy and sell and cap from previous question 
- AlSOOOOO one more way to solve this
- Using dp(n)(4) ---- Basically each trans is taken here and odd / even is counted as buy or not buy (pretty smart)


```
public static int maxProfit(int[] prices) {  
    int n = prices.length;  
    int[][][] dp = new int[n + 1][2][3];  
    for(int idx = n - 1; idx >= 0; idx--){  
        for(int buy = 0; buy < 2; buy++){  
            for(int cap = 1; cap < 3; cap++){  
                int best = 0;  
                if(buy == 1){  
                    int keepit = dp[idx + 1][buy][cap];  
                    int sellit = prices[idx] + dp[idx + 1][0][cap - 1];  
                    best = Math.max(keepit, sellit);  
                }else{  
                    int moveon = dp[idx + 1][buy][cap];  
                    int buyon = -prices[idx] + dp[idx + 1][1][cap];  
                    best = Math.max(moveon, buyon);  
                }  
                dp[idx][buy][cap] = best;  
            }  
        }  
    }  
    return dp[0][0][2];  
}
```