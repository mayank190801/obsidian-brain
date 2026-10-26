[[DSA]]
[[Dynamic Programming DSA]]

[Edit Distance - Naukri Code 360](https://www.naukri.com/code360/problems/edit-distance_630420?source=youtube&campaign=striver_dp_videos&utm_source=youtube&utm_medium=affiliate&utm_campaign=striver_dp_videos&leftPanelTabValue=SUBMISSION)


- Beautiful Edge case which I actually missed while solving the problem
- What would happen if i == -1 or j == -1 (get this correct for both of them)
- At max you can improve the below code 2 1D array and nothing else 

```
 public static int editDistance(String str1, String str2) {
        int n = str1.length();
        int m = str2.length();
        int[][] dp = new int[n + 1][m + 1];
        for(int i = 0; i <= m; i++){
            dp[0][i] = i;
        }
        for(int i = 0; i <= n; i++){
            dp[i][0] = i;
        }

        for(int i = 1; i <= n; i++){
            for(int j = 1; j <= m; j++){
                if(str1.charAt(i - 1) != str2.charAt(j - 1)){
                    int delete = dp[i - 1][j] + 1;
                    int insert = dp[i][j - 1] + 1;
                    int replace = dp[i - 1][j - 1] + 1;
                    dp[i][j] = Math.min(delete, Math.min(insert, replace));
                }else{
                    dp[i][j] = dp[i - 1][j - 1];
                }
            }
        }

        return dp[n][m];
    }
```