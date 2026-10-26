[[DSA]]
[[Dynamic Programming DSA]]

[Maximum Path Sum in the matrix - Naukri Code 360](https://www.naukri.com/code360/problems/maximum-path-sum-in-the-matrix_797998?source=youtube&campaign=striver_dp_videos&utm_source=youtube&utm_medium=affiliate&utm_campaign=striver_dp_videos&leftPanelTabValue=SUBMISSION)

```
public static int getMaxPathSum(int[][] matrix) {  
    int n = matrix.length;  
    int m = matrix[0].length;  
  
    int[][] dp = new int[n][m];  
    for(int i = n - 1; i >= 0; i--){  
        for(int j = 0; j < m; j++){  
            if(i == n - 1){  
                dp[i][j] = matrix[i][j];  
            }else{  
                //teen directions mein search maaro answer ke liye   
int best = Integer.MIN_VALUE;  
                for(int k = -1; k <= 1; k++){  
                    int value;  
                    if(j + k < 0 || j + k >= m) value = Integer.MIN_VALUE;  
                    else value = dp[i + 1][j + k];  
                    best = Math.max(best, value);  
                }  
                dp[i][j] = best + matrix[i][j];  
            }  
        }  
    }  
  
    int best = Integer.MIN_VALUE;  
    for(int i = 0; i < matrix[0].length; i++){  
        best = Math.max(best,dp[0][i]);  
    }  
  
    return best;  
}
```

- The core is writing a beautiful recursive solution, what I did is simply if the index is out of the bound return the smallest value possible! 
- If the index is greater than n - 1 return 0 
- And that's it! (You can even space optimise the above solution if you want but I would be moving ahead now)

Recursion complexities 
TC  - O(3 ^ n)
SC - O(n) 
