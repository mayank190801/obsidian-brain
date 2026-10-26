[[DSA]]
[[Dynamic Programming DSA]]

[Print all LCS sequences | Practice | GeeksforGeeks](https://www.geeksforgeeks.org/problems/print-all-lcs-sequences3413/0)

![[Screenshot 2024-08-26 at 6.51.29 AM.png]]

```

class Solution {
    public List<String> all_longest_common_subsequences(String s, String t) {
        //ye graph bnalo ek baari ko 
        //fir ek baari ko 
        int n = s.length();
        int m = t.length();
        int[][] dp = new int[n + 1][m + 1];
        for(int i = 1; i <= n; i++){
            for(int j = 1; j <= m; j++){
                if(s.charAt(i - 1) == t.charAt(j - 1)){
                    dp[i][j] = dp[i - 1][j - 1] + 1;
                }else{
                    dp[i][i] = Math.max(dp[i - 1][j], dp[i][j - 1]);
                }
            }
        } 
        StringBuilder sb = new StringBuilder();
        int i = n;
        int j = m;
        while(i > 0 && j > 0){
            if(s.charAt(i - 1) == t.charAt(j - 1)){
                sb.append(s.charAt(i - 1));
                i--;
                j--;
            }else{
                if(dp[i - 1][j] > dp[i][j - 1]){
                    i--;
                }else{
                    j--;
                }
            }
        }
        List<String> ans = new ArrayList<>();        
        ans.add(sb.reverse().toString());
        return ans;
    }
}
```

- Basically if two character matches, then go i -1 and j - 1
- If not matches then go towards the higher side 