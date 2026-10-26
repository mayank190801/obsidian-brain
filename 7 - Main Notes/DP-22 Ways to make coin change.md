[[DSA]]
[[Dynamic Programming DSA]]

[Ways To Make Coin Change - Naukri Code 360](https://www.naukri.com/code360/problems/ways-to-make-coin-change_630471?source=youtube&campaign=striver_dp_videos&utm_source=youtube&utm_medium=affiliate&utm_campaign=striver_dp_videos&leftPanelTabValue=PROBLEM)

```
    public static long countWaysToMakeChange(int denominations[], int value){
        int n = denominations.length;
        long[] prev = new long[value + 1];
        long[] curr = new long[value + 1];
        prev[0] = 1;
        for(int i = 1; i <= n; i++){
            for(int j = 0; j <= value; j++){
                long notTake = prev[j];
                long take = 0;
                if(j - denominations[i - 1] >= 0) take = curr[j - denominations[i - 1]];
                curr[j] = take + notTake;
            }
            long[] temp = curr;
            curr = prev;
            prev = temp;
        }
        return prev[value];
    }
```

-- pretty basic logic?? (not much learned from this one?)