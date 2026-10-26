[[DSA]]
[[Dynamic Programming DSA]]

[Unique Paths - Naukri Code 360](https://www.naukri.com/code360/problems/total-unique-paths_1081470?source=youtube&campaign=striver_dp_videos&utm_source=youtube&utm_medium=affiliate&utm_campaign=striver_dp_videos&leftPanelTabValue=PROBLEM)

```
public static int uniquePaths(int m, int n) {  
    int[] dp = new int[n + 1];  
    int[] ndp = new int[n + 1];  
    ndp[1] = 1;  
    for(int i = 1; i <= m; i++){  
        for(int j = 1; j <= n; j++){  
            if(i == 1 && j == 1) continue;  
            ndp[j] = dp[j] + ndp[j - 1];  
        }  
        int[] temp = dp;  
        dp = ndp;  
        ndp = temp;  
    }  
    return dp[n];  
}
```

Damnnnn, always a firyyy question for sureeee 

-> Definitely solve the final version of the problem where we have space optimised it 
-> Now with two dp, you have to actually see what they fetch and and how they fetch!!! 
-> Like ndp not only depend on dp, but also npd itself
-> Also which value to have default value and so on.... 

- Overall basic logic, but pretty fun to solve in real 

Complexity for Recursion 
TC - 2 ^ (m + n)
SC - Path length (recursion stack will never be longer than that )


