[[DSA]]
[[Dynamic Programming DSA]]

- Really good question 
- Keep a count array and update it while you are creating the solution for LIS 
- Rather than bracktracking, just create the answer while creating the LIS

https://www.naukri.com/code360/problems/number-of-longest-increasing-subsequence_3751627?source=youtube&campaign=striver_dp_videos&utm_source=youtube&utm_medium=affiliate&utm_campaign=striver_dp_videos&leftPanelTabValue=SUBMISSION


```
public static int findNumberOfLIS1(int []arr) {
        int n = arr.length;
        int[] lis = new int[n];
        int[] cnt = new int[n];

        int idx = 0;
        for(int i = 0; i < n; i++){
            lis[i] = 1;
            cnt[i] = 1;
            for(int j = 0; j < i; j++){
                if(arr[i] > arr[j]){
                    int get = lis[j] + 1;
                    if(get > lis[i]){
                        lis[i] = get;
                        cnt[i] = cnt[j];
                    }else if(get == lis[i]){
                        cnt[i] += cnt[j];
                    }
                }
            }
            if(lis[i] > lis[idx]){
                idx = i;
            }
        }

        int ans = 0;
        for(int i = 0; i < n; i++){
            if(lis[i] == lis[idx]){
                ans += cnt[i];
            }
        }

        return ans;
    }
```