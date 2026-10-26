
Tags : [[Dynamic Programming DSA]]

- My Solution 
- Space Optimised Solution 

- So using DP you can get the answer for i, j (simple as that)
- Just get the answer possible for current, and what is the possible answer for i+1, j+1

```java
class Solution {
public int maximalSquare(char[][] matrix) {
        int n = matrix.length;
        int m = matrix[0].length;

        int[][] horizontal = new int[n + 1][m + 1];
        int[][] vertical = new int[n + 1][m + 1];

        for(int i = n - 1; i >= 0; i--){
            for(int j = m - 1; j >= 0; j--){
                if(matrix[i][j] == '1'){
                    horizontal[i][j] = horizontal[i][j + 1] + 1;
                    vertical[i][j] = vertical[i + 1][j] + 1;
                }
            }
        }
        
        int ans = 0;
        int[][] dp = new int[n + 1][m + 1];
        
        for(int i = n - 1; i >= 0; i--){
            for(int j = m - 1; j >= 0; j--){            
                int minSquare = Math.min(horizontal[i][j], vertical[i][j]);         
                int minSquarePossibleForChild = dp[i + 1][j + 1] + 1;
                dp[i][j] = Math.min(minSquare, minSquarePossibleForChild);
                ans = Math.max(ans, dp[i][j]);
            }
        }
            
        return ans * ans;
    }
}
```


Space Optimised Solution 
```java
	public int maximalSquare(char[][] matrix) {
        int n = matrix.length;
        int m = matrix[0].length;
        int ans = 0;
        int[][] dp = new int[n + 1][m + 1];
        
        for(int i = n - 1; i >= 0; i--){
            for(int j = m - 1; j >= 0; j--){            
                if(matrix[i][j] != '1') continue;
                int minSquare = Math.min(dp[i+1][j] + 1, dp[i][j+1] + 1);         
                int minSquarePossibleForChild = dp[i + 1][j + 1] + 1;
                dp[i][j] = Math.min(minSquare, minSquarePossibleForChild);
                ans = Math.max(ans, dp[i][j]);
            }
        }
            
        return ans * ans;
    }
```