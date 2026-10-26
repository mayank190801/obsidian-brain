[[DSA]]
[[Dynamic Programming DSA]]

https://www.naukri.com/code360/problems/longest-bitonic-sequence_1062688?source=youtube&campaign=striver_dp_videos&utm_source=youtube&utm_medium=affiliate&utm_campaign=striver_dp_videos&leftPanelTabValue=SUBMISSION


```
public static int longestBitonicSequence(int[] arr, int n) {
        int[] inc = new int[n];
        int[] dec = new int[n];

        lis(arr, inc, n);
        reverse(arr);
        lis(arr, dec, n);
        reverse(dec);

        int ans = 0;
        for(int i = 0; i < n; i++){
            ans = Math.max(ans, inc[i] + dec[i] - 1);
        }

        return ans;
    }

    public static void lis(int[] arr, int[] dp, int n){
        for(int i = 0; i < n; i++){
            int best = 0;
            for(int j = 0; j < i; j++){
                if(arr[i] > arr[j]){
                    best = Math.max(best, dp[j]);
                }
            }
            dp[i] = best + 1;
        }
    }
```