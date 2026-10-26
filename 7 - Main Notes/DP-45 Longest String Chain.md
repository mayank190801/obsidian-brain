[[DSA]]
[[Dynamic Programming DSA]]

https://www.naukri.com/code360/problems/longest-string-chain_3752111?source=youtube&campaign=striver_dp_videos&utm_source=youtube&utm_medium=affiliate&utm_campaign=striver_dp_videos&leftPanelTabValue=SUBMISSION

- Just similar to LIS 

```
 public static int longestStrChain1(String[] arr) {
        int n = arr.length;
        int[] dp = new int[n];

        Arrays.sort(arr, (a, b) -> a.length() - b.length());
    
        int ans = 0;
        for(int i = 0; i < n; i++){
            int best = 0;
            for(int j = 0; j < i; j++){
                if(successor(arr[j], arr[i])){
                    if(dp[j] > best){
                        best = dp[j];
                    }
                }
            }
            dp[i] = best + 1;
            if(dp[i] > dp[ans]){
                ans = i;
            }
        }

        return dp[ans];
    }

  public static boolean successor(String a, String b){
        if(b.length() - a.length() != 1) return false;
        int idxa = 0;
        int idxb = 0;
        
        while(idxa < a.length() && idxb < b.length()){
            if(a.charAt(idxa) == b.charAt(idxb)){
                idxa++;
            }
            idxb++;
        }
        
        return idxa == a.length();
    }
```