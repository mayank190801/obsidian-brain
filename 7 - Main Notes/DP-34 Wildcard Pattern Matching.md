[[DSA]]
[[Dynamic Programming DSA]]

[Wildcard Pattern Matching - Naukri Code 360](https://www.naukri.com/code360/problems/wildcard-pattern-matching_701650?source=youtube&campaign=striver_dp_videos&utm_source=youtube&utm_medium=affiliate&utm_campaign=striver_dp_videos&leftPanelTabValue=SUBMISSION)

Learnings to take away from this question --

- If you are doing i - 1, j and i, j - 1. (Then you don't have to do i - 1, j - 1) - because it will be covered in it only.
- Think about base cases with S1 < 0 what happens and S2 < 0 what happens 
- Below question be even more space optimised (its upto you if you want to or not)

```
public static boolean wildcardMatching(String pattern, String text) {  
    int n = pattern.length();  
    int m = text.length();  
    boolean[][] dp = new boolean[n + 1][m + 1];  
  
    dp[0][0] = true;  
    for(int i = 1; i <= n; i++){  
        if(pattern.charAt(i - 1) != '*') break;  
        dp[i][0] = true;  
    }  
  
    for(int i = 1; i <= n; i++){  
        for(int j = 1; j <= m; j++){  
            if(pattern.charAt(i - 1) == text.charAt(j - 1) || pattern.charAt(i - 1) == '?'){  
                dp[i][j] = dp[i - 1][j - 1];  
            }  
            if(pattern.charAt(i - 1) == '*'){  
                dp[i][j] = dp[i - 1][j] || dp[i][j - 1];  
            }  
        }  
    }  
return dp[n][m];
```