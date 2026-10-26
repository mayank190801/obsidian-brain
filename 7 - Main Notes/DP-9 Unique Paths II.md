[[DSA]]
[[Dynamic Programming DSA]]

[Unique Paths II - Naukri Code 360](https://www.naukri.com/code360/problems/maze-obstacles_977241?source=youtube&campaign=striver_dp_videos&utm_source=youtube&utm_medium=affiliate&utm_campaign=striver_dp_videos&leftPanelTabValue=SUBMISSION)

```
static int mazeObstacles(int m, int n, ArrayList<ArrayList<Integer>> mat) {  
    int modulo = 1_000_000_007;  
    int[][] dp = new int[m + 1][n + 1];  
    for(int i = 1; i <= m; i++){  
        for(int j = 1; j <= n; j++){  
            if(mat.get(i - 1).get(j - 1) == -1)  continue;  
            if(i == 1 && j == 1){  
                dp[i][j] = 1;  
                continue;  
            }  
            dp[i][j] = (dp[i - 1][j] + dp[i][j - 1])%modulo;  
        }  
    }  
    return dp[m][n]%modulo;  
}
```

- Just add one more conditional check in here (that's it)
- Very similar to previous one, also add modulo concept if you can 
