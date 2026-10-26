[[DSA]]
[[Dynamic Programming DSA]]

https://www.naukri.com/code360/problems/highway-billboards_3125969?source=youtube&campaign=striver_dp_videos&utm_source=youtube&utm_medium=affiliate&utm_campaign=striver_dp_videos&leftPanelTabValue=PROBLEM

-- Learnings --- 
- You are an idiot, no need of another cooldown vairable 
- Just when you sell, pick the answer from idx + 2 and not idx + 1 (that's it)
- Also you can convert it to 3 - 1D dp solution (since you want idx, idx + 1 and idx + 2)
- One more improvement would be to remove for loop for buy (PRETTY COOL)

```
  public static int stockProfit(int[] prices) {
        return recurProfit(prices, 0, 0, 0);
    }

    public static int recurProfit(int[] prices, int idx, int buy, int cooldown){
        int n = prices.length;
        if(idx == n) return 0;

        int best = 0;
        if(buy == 1){
            //already bought
            int keepit = recurProfit(prices, idx + 1, buy, cooldown - 1);
            int sellit = prices[idx] + recurProfit(prices, idx + 1, 0, 1);
            best = Math.max(keepit, sellit);
        }else{
            int keepit = recurProfit(prices, idx + 1, buy, cooldown - 1);
            int buyit = 0;
            if(cooldown <= 0){
                buyit = -prices[idx] + recurProfit(prices, idx + 1, 1, cooldown);
            }
            best = Math.max(keepit, buyit);
        }

        return best;
    }
```