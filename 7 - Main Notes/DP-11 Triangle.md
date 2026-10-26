[[DSA]]
[[Dynamic Programming DSA]]

[Triangle - Naukri Code 360](https://www.naukri.com/code360/problems/triangle_1229398?source=youtube&campaign=striver_dp_videos&utm_source=youtube&utm_medium=affiliate&utm_campaign=striver_dp_videos&leftPanelTabValue=PROBLEM)

```
public static int minimumPathSum(int[][] triangle, int n) {  
    int[] prev = new int[n + 1];  
    int[] curr = new int[n + 1];  
    for(int i = n - 1; i >= 0; i--){  
        for(int j = 0; j <= i; j++){  
            curr[j] = Math.min(prev[j], prev[j + 1]) + triangle[i][j];  
        }  
        int[] temp = curr;  
        curr = prev;  
        prev = temp;  
    }  
    return prev[0];  
}
```

- Just keep the question the simplest you can start 
- In this you could have done top down to bottom up approach. 

- I went with the easiest approach for recursion (i.e starting from the top)
- Also the dp recursion was bottom up (and that was simple as well, as you can see)
