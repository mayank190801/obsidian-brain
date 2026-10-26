[[DSA]]
[[Dynamic Programming DSA]]

[Unbounded Knapsack - Naukri Code 360](https://www.naukri.com/code360/problems/unbounded-knapsack_1215029?source=youtube&campaign=striver_dp_videos&utm_source=youtube&utm_medium=affiliate&utm_campaign=striver_dp_videos&leftPanelTabValue=SUBMISSION)


```
public static int unboundedKnapsack(int n, int w, int[] profit, int[] weight) {
        int[] curr = new int[w + 1];
        int[] prev = new int[w + 1];
        for(int i = 1; i <= n; i++){
            for(int j = 0; j <= w; j++){
                int notTake = prev[j];
                int take = 0;
                if(j - weight[i - 1] >= 0) take = curr[j - weight[i - 1]] + profit[i - 1];
                curr[j] = Math.max(take, notTake);
            }
            int[] temp = curr;
            curr = prev;
            prev = temp;
        }
        return prev[w];
    }
```

-- no base cases as per (if idx < 0) return 0; (this is for both knapsack and unbounded knapsack)
-- because of which we just have to increase the dp size by 1 (so that we can handle idx < 0) scenarios 

- Other than pretty obvious solution, nothing exciting in this problem as well 
------------

WAITING A FUCK 
We can space optimise it even further no?? 
YES YES YES YES PRETTY INSANE SPACE OPTIMISATION 

--- you at any point, require the above array above index only and current array previous indexes 
- That could be done with 1D array as well 

```
    public static int unboundedKnapsack(int n, int w, int[] profit, int[] weight) {
        int[] curr = new int[w + 1];
        for(int i = 1; i <= n; i++){
            for(int j = 0; j <= w; j++){
                int notTake = curr[j];
                int take = 0;
                if(j - weight[i - 1] >= 0) take = curr[j - weight[i - 1]] + profit[i - 1];
                curr[j] = Math.max(take, notTake);
            }
        }
        return curr[w];
    }
```

Hence the above solution works beautifully (just see what states you are hitting and if you can reduce the array size for storing previous answer )





