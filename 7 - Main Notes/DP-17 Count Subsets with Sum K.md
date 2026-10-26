[[DSA]]
[[Dynamic Programming DSA]]

https://www.naukri.com/code360/problems/number-of-subsets_3952532?source=youtube&campaign=striver_dp_videos&utm_source=youtube&utm_medium=affiliate&utm_campaign=striver_dp_videos


```
public static int findWays(int num[], int tar) {
        int n = num.length;
        int modulo = 1_000_000_007;

        int[] prev = new int[tar + 1];
        int[] curr = new int[tar + 1];
        prev[0] = 1;

        for(int i = 1; i <= n; i++){
            for(int j = 0; j <= tar; j++){
                int notTake = prev[j];
                int take = 0;
                if(j - num[i - 1] >= 0) take = prev[j - num[i - 1]];
                curr[j] = (take + notTake) % modulo;
            }
            int[] temp = prev;
            prev = curr;
            curr = temp;
        }

        return prev
```

- Above solution is the best possible solution for this question 
- In this if you notice I have taken i from 1 to n because (i == 0) is considered as i < 0 basically , 
- We could have done something different as well, but this seemed to be appropriate to me\

Recursion 

```
   public static int recurFindWays(int[] num, int tar, int idx, int[][] dp){
        int modulo = 1_000_000_007;
        if(idx < 0){
            if(tar == 0) return 1;
            return 0;
        }
        if(dp[idx][tar] != -1) return dp[idx][tar];

        int notTake = recurFindWays(num, tar, idx - 1, dp);
        int take = 0;
        if(tar - num[idx] >= 0) take = recurFindWays(num, tar - num[idx], idx - 1, dp);

        return dp[idx][tar] = (notTake + take) % modulo;
    }
```

In the above question if suppose negative numbers are also there as sum? 
Then what we would have done?? (think about that case once)