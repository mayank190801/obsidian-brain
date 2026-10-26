[[DSA]]
[[Dynamic Programming DSA]]

- This problem is similar to fibonacci only 
- You can solve it both from left to right and right to left 

```java
class Solution {
    public int climbStairs(int n) {
        int[] dp = new int[n + 1];
        dp[0] = 1; dp[1] = 1;
        for(int i = 2; i <= n; i++){
            dp[i] = dp[i - 2] + dp[i - 1];
        }
        return dp[n];
    }
}

-- Just one difference is that dp[0] = 1 
```

