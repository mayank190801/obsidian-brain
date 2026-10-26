[[DSA]]

[[Dynamic Programming DSA]]

[Print all LCS sequences | Practice | GeeksforGeeks](https://www.geeksforgeeks.org/problems/print-all-lcs-sequences3413/0)

```
public static List<String> all_longest_common_subsequences(String s, String t) {
        int n = s.length();
        int m = t.length();
        int[][] dp = new int[n + 1][m + 1];
        for(int i = 1; i <= n; i++){
            for(int j = 1; j <= m; j++){
                if(s.charAt(i - 1) == t.charAt(j - 1)){
                    dp[i][j] = dp[i - 1][j - 1] + 1;
                }else{
                    dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
                }
            }
        }
//        for(int i = 0; i <= n ; i++){
//            for(int j = 0; j <= m; j++){
//                System.out.print(dp[i][j] + " ");
//            }
//            System.out.println();
//        }
        Set<String> set = new HashSet<>();
        Set<String> extraCompCheck = new HashSet<>();
        List<String> ans = new ArrayList<>();
        StringBuilder sb = new StringBuilder();
        recurLongSub(s, t, dp, n, m, ans, sb, set, extraCompCheck);
        Collections.sort(ans);
        return ans;
    }

    //should be backtracking and remove what not if you want
    //recursion stack space might not be issue for sure, going to find the same answer again and again might be the issue
    //i j and curr is same, return the created the answer only - simple
    //like isme bhi dp lgalo
    public static void recurLongSub(String s, String t, int[][] dp, int i, int j, List<String> ans, StringBuilder curr, Set<String> set, Set<String> extraCompCheck){
        if(i == 0 || j == 0) {
            String fcurr = curr.reverse().toString();
            curr.reverse();
            if(set.contains(fcurr)) return;
            set.add(fcurr);
            ans.add(fcurr);
            return;
        }

        //if i j str (already reached then don't move forward, otherwise mark true
        String checker = i + "," + j + "," + curr.toString();
        if(extraCompCheck.contains(checker)) return;
        extraCompCheck.add(checker);

        if(s.charAt(i - 1) == t.charAt(j - 1)){
            curr.append(s.charAt(i - 1));
            recurLongSub(s, t, dp, i - 1, j - 1, ans, curr, set, extraCompCheck);
            curr.deleteCharAt(curr.length() - 1);
        }else{
            if(dp[i - 1][j] >= dp[i][j - 1]) {
                recurLongSub(s, t, dp, i - 1, j, ans, curr, set, extraCompCheck);
            }
            if(dp[i - 1][j] <= dp[i][j - 1]){
                recurLongSub(s, t, dp, i, j - 1, ans, curr, set, extraCompCheck);
            }
        }
    }
```


-- INSANE THINGS TO LEARN FROM THIS ONE 

- first simple creating the dp for the longest common subsequence 
- Afterwards create the recursion logic to get the subsequence 
- Also some cleaner way to write >= and stuff (really comment sections always makes you a better and cleaner coder I believe)
- And then again reducing extra computation to pass all the test cases 



