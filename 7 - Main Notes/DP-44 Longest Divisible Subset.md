[[DSA]]
[[Dynamic Programming DSA]]

https://www.naukri.com/code360/problems/divisible-set_3754960?source=youtube&campaign=striver_dp_videos&utm_source=youtube&utm_medium=affiliate&utm_campaign=striver_dp_videos&leftPanelTabValue=SUBMISSION

- So basically same as LIS 
- You also create a idx array for the creation of answer
- MOST IMPORTANT - DONT FORGET TO SORT THE ARRAY (otherwise you won't be able to get the right answers)

```
    public static List< Integer > divisibleSet(int []arr) {
        int n = arr.length;
        int[] dp = new int[n];
        int[] idx = new int[n];

        Arrays.sort(arr);

        int ans = 0;
        for(int i = 0; i < n; i++){
            int best = 0;
            int hash = -1;
            for(int j = 0; j < i; j++){
                if(arr[i] % arr[j] == 0 || arr[j] % arr[i] == 0){
                    if(dp[j] > best){
                        best = dp[j];
                        hash = j;
                    }
                }
            }
            dp[i] = best + 1;
            idx[i] = hash;
            
            if(dp[i] > dp[ans]){
                ans = i;
            }
        }

        List<Integer> fans = new ArrayList<>();
        while(ans != -1){
           fans.add(arr[ans]);
           ans = idx[ans];
        }

        Collections.sort(fans);
        return fans;
    }
```