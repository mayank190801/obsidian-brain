[[DSA]]
[[Dynamic Programming DSA]]

[Ninja’s Training - Naukri Code 360](https://www.naukri.com/code360/problems/ninja-s-training_3621003?source=youtube&campaign=striver_dp_videos&utm_source=youtube&utm_medium=affiliate&utm_campaign=striver_dp_videos&leftPanelTabValue=PROBLEM)

```
public static int ninjaTraining(int n, int points[][]) {  
    int[] dp = new int[3];  
    int[] ndp = new int[3];  
  
    for(int i = 1; i <= n; i++){  
        for(int j = 0; j < 3; j++){  
            int best = 0;  
            for(int k = 0; k < 3; k++){  
                if(j == k) continue;  
                best = Math.max(best, dp[k]);  
            }  
            ndp[j] = best + points[i - 1][j];  
        }  
        int[] temp = dp;  
        dp = ndp;  
        ndp = temp;  
    }  
    return Math.max(dp[0], Math.max(dp[1], dp[2]));  
}
```

Always first check if the greedy fails or not 
Now get an example where greedy fails brother (pretty easy)

1000000 1 1 
2 1 1 
1 2 1  

(simple example of greedy failing)

The above code is the final boss basically 
-> First the recursion logic is pretty simple to write (just get the best answer by getting the previous best and adding the current one)
-> Then apply memoization 
-> Then for loop sort of dp, and after that improve it even better by using even less space!! (insane)


2D dp good practise problem
