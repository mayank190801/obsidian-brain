[[DSA]]
[[Dynamic Programming DSA]]

[Best Time to Buy and Sell Stock II - Naukri Code 360](https://www.naukri.com/code360/problems/selling-stock_630282?source=youtube&campaign=striver_dp_videos&utm_source=youtube&utm_medium=affiliate&utm_campaign=striver_dp_videos&leftPanelTabValue=SUBMISSION)

learning --  (a lot of them)
- You could have buy as Idx (which you tried) or have it as 1 / 0 (better)
- Just create the answer till present situation!!! (if you bought it, reduce your profits man!!!)
- You can solve it with 4 variables as well (or 2 - 2 spaced array) 
- Starting from start to end in recursion (reverse for tabulation)

```
public static long getMaximumProfit (int n, long[] values) {  
   long[] ahead = new long[2];  
   long[] prev = new long[2];  
  
   for(int idx = n - 1; idx >= 0; idx--){  
       for(int buy = 0; buy <= 1; buy++){  
           long best = 0;  
           if(buy == 1){  
               long keepit = ahead[buy];  
               long sellit = values[idx] + ahead[0];  
               best = Math.max(keepit, sellit);  
           }else{  
               long moveon = ahead[buy];  
               long buyon = -values[idx] + ahead[1];  
               best = Math.max(moveon, buyon);  
           }  
           prev[buy] = best;  
       }  
       long[] temp = ahead;  
       ahead = prev;  
       prev = temp;  
   }  
   return ahead[0];  
}
```