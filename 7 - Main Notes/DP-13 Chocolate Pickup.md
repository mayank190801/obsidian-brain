
[[DSA]]
[[Dynamic Programming DSA]]

[Chocolate Pickup - Naukri Code 360](https://www.naukri.com/code360/problems/ninja-and-his-friends_3125885?source=youtube&campaign=striver_dp_videos&utm_source=youtube&utm_medium=affiliate&utm_campaign=striver_dp_videos&leftPanelTabValue=SUBMISSION)

```
public static int maximumChocolates(int r, int c, int[][] grid) {  
    int[][] curr = new int[c + 1][c + 1];  
    int[][] prev = new int[c + 1][c + 1];  
  
    for(int i = r - 1; i >= 0; i--){  
        for(int j1 = 0; j1 < c; j1++){  
            for(int j2 = 0; j2 < c; j2++){  
  
                int best = 0;  
                for(int j = -1; j <= 1; j++){  
                    for(int k = -1; k <= 1; k++){  
                        int nj1 = j1 + j;  
                        int nj2 = j2 + k;  
                        int val;  
                        if(nj1 < 0 || nj1 >= c || nj2 < 0 || nj2 >= c) val = 0;  
                        else val = prev[nj1][nj2];  
  
                        best = Math.max(best, val);  
                    }  
                }  
  
                int currentPick = (j1 == j2) ? grid[i][j1] : grid[i][j1] + grid[i][j2];  
                curr[j1][j2] = currentPick + best;  
            }  
        }  
          
        int[][] temp = curr;  
        curr = prev;  
        prev = temp;  
    }  
  
    return prev[0][c - 1];  
}
```

---- ONE OF THE BEST QUESTIONS OUT THERE FOR RECURSION ----- (no caps)
-- God of 3D dp question

For the above question, writing the recurrence relation is the most important part

best = (j1 == j2) then return single vaue, otherwise some of both indexes  + recurrence(i , j1 + (all three possible states), j2 + (all three possible states));

THE RECCURRENCE IS SO GOOOODDDDD!!!! 

After that is simple 3D dp, which you can convert to 2D or whatever 

TC for recurrence should be - O(9^n)
Space Complexity - O(N)  --- Only stack space is used in here!

TC for best case solution - O(NxMxM)
Space Complexity - O(MxM)