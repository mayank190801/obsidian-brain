[[DSA]]
[[Dynamic Programming DSA]]

[Minimum Path Sum - Naukri Code 360](https://www.naukri.com/code360/problems/minimum-path-sum_985349?source=youtube&campaign=striver_dp_videos&utm_source=youtube&utm_medium=affiliate&utm_campaign=striver_dp_videos&leftPanelTabValue=SUBMISSION)

```
public static int minSumPath(int[][] grid) {  
    int n = grid.length;  
    int m = grid[0].length;  
  
    int[] prev = new int[m + 1];  
    int[] curr = new int[m + 1];  
      
    for(int i = 1; i <= n; i++){  
        for(int j = 1; j <= m; j++){  
           if(i == 1 && j == 1) {  
               curr[j] = grid[0][0];  
               continue;  
           }  
            int left = j == 1 ? Integer.MAX_VALUE : curr[j - 1];  
            int top = i == 1 ? Integer.MAX_VALUE : prev[j];  
            curr[j] = Math.min(left, top) + grid[i - 1][j - 1];  
        }  
          
        int[] temp = prev;  
        prev = curr;  
        curr = temp;  
    }  
  
    return prev[m];  
}
```

-> If the edge cases in min path and all question, try using the logic there itself, rather than leaving it for recursion to solve 
-> Like here I could have gotten Integer.MAX_VALUE from recursion base cases only, but then it would have increase the complexity (hence keep it simple)

