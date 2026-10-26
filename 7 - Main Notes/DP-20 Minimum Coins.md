[[DSA]]
[[Dynamic Programming DSA]]

[Minimum Elements - Naukri Code 360](https://www.naukri.com/code360/problems/minimum-elements_3843091?leftPanelTab=1%3Fsource%3Dyoutube&campaign=striver_dpseries&utm_source=youtube&utm_medium=affiliate&utm_campaign=striver_dpseries&leftPanelTabValue=SUBMISSION)

```
    public static int minimumElements(int num[], int x) {
        int n = num.length;
        int[] prev = new int[x + 1];
        int[] curr = new int[x + 1];
        //what is it reaching out to?
        for(int i = 1; i <= x; i++){
            prev[i] = 1_000_000_000;
        }
        for(int i = 1; i <= n; i++){
            for(int j = 0; j <= x; j++){
                int notTake = prev[j];
                int take = Integer.MAX_VALUE - 1;
                if(j - num[i - 1] >= 0){
                    take = curr[j - num[i - 1]] + 1;
                }

                curr[j] = Math.min(notTake, take);
            }

            int[] temp = prev;
            prev = curr;
            curr = temp;
        }
        return prev[x] >= 1_000_000_000 ? -1: prev[x];
    
```

- important learnings from this question 
- You can avoid using Integer.MAX_VALUE and use 10e9 instead (if the max answer is not bigger than that ofc)


ALSO for recursion based solution ----  (not accurate would work for this one)
- In the above recursion based solution for this question 

TC - O (>>>> 2^n) --- exponential (no need to find out the exact just say exponential and you are good with it) -- also at every index we have more than 2 options in this one 
SC - O(>>> N) -- auxilary space is also greater than N (because i can be repeated several thousand times as well, not depended on idx, more like the x);



