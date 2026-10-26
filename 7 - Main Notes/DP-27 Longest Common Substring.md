[[DSA]]
[[Dynamic Programming DSA]]

[DP 27. Longest Common Substring | DP on Strings 🔥 (youtube.com)](https://www.youtube.com/watch?v=_wP9mWNPL5w&list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY&index=28)

```
 public static int lcs(String s, String t){
        int n = s.length();
        int m = t.length();
        int best = 0;
        int[][] dp = new int[n + 1][m + 1];
        for(int i = 1; i <= n; i++){
            for(int j = 1; j <= m; j++){
                if(s.charAt(i - 1) == t.charAt(j - 1)){
                    dp[i][j] = dp[i - 1][j - 1] + 1;
                }else{
                    dp[i][j] = 0;
                }
                best = Math.max(dp[i][j], best);
            }
        } 
        return best;
    }
```

- Simple just one change in LCS (rather than max now return 0)
- ALSO KEEP TRACK OF THE BEST ANSWER YET (simple)
- You can space optimize the above solution a bit more 


