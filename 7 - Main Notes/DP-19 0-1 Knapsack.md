[[DSA]]
[[Dynamic Programming DSA]]

[0 1 Knapsack - Naukri Code 360](https://www.naukri.com/code360/problems/0-1-knapsack_920542?source=youtube&campaign=striver_dp_videos&utm_source=youtube&utm_medium=affiliate&utm_campaign=striver_dp_videos&leftPanelTabValue=SUBMISSION)

(insane)

```
	static int knapsack(int[] weight, int[] value, int n, int maxWeight) {
        int[] curr = new int[maxWeight + 1];
        for(int i = 1; i <= n; i++){
            for(int j = maxWeight; j >= 0; j--){
                int notTake = curr[j];
                int take = 0;
                if(j - weight[i - 1] >= 0) take = curr[j - weight[i - 1]] + value[i - 1];
                curr[j] = Math.max(take, notTake);
            }
        }
        return curr[maxWeight];
    }
```

- Above solution is years of efforts and development 
- First recursion 
- Then memoization 
- Then tabulation 
- Then space optimisaiton iwth prev and curr array 
- THEN EVEN REMOVING THOSE ARRAYS!!!! (HOW CRAZYYYYY)

Big Question
- How were you able to remove the space? 
- So basically if you notice the tabulation and answer creation 
- You were always completely dependent on previous array + only the elements <= j (currentWeight)
- So if you just traverse from right to left rather than left to right (it solves that problem of updating the previous answer) --- THINK ABOUT IT CRAZY 