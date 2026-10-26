[[DSA]]
[[Dynamic Programming DSA]]

[DP 35. Best Time to Buy and Sell Stock | DP on Stocks 🔥 (youtube.com)](https://www.youtube.com/watch?v=excAOvwF_Wk&list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY&index=36)

- keep the minimum at every point 

```
public static int maximumProfit(ArrayList<Integer> prices){  
    int ans = 0;  
    int curr = prices.get(0);  
    for(int i = 0; i < prices.size(); i++){  
        curr = Math.min(curr, prices.get(i));  
        ans = Math.max(ans, prices.get(i) - curr);  
    }  
    return ans;  
}
```