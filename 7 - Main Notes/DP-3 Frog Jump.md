
[[DSA]]
[[Dynamic Programming DSA]]

Problem Link - https://www.naukri.com/code360/problems/frog-jump_3621012

- You can solve from left to right and right to left (your choice, your call)
### Why are greedy solution doesn't work here? (important)

30 10 60 10 60 50 
- Try jumping to lowest distance 
- Also now trying through best answer (hence have to try all possible ways)

Similar to Fibonacci, but the concept of minimum introduces typical edge cases 
- You can solve that using Integer.MAX_VALUE in long world 
- You can solve the edge cases indiviually

```
public static int frogJump(int n, int heights[]) {  
  
    long ahead = 0;  
    long aheadahead = 0;  
    for(int curr = n - 2; curr >= 0; curr--){  
        long oneLevel = Integer.MAX_VALUE;  
        if(curr <= n-2) oneLevel = Math.abs(heights[curr] - heights[curr + 1]) + ahead;  
  
        long secondLevel = Integer.MAX_VALUE;  
        if(curr <= n-3) secondLevel = Math.abs(heights[curr] - heights[curr + 2]) + aheadahead;  
  
        aheadahead = ahead;  
        ahead = Math.min(oneLevel, secondLevel);  
  
    }  
    return (int) ahead;  
}
```

### Follow up Question 

- Solve it for k jumps , rather than only 1 and 2 
- Simply use for loop 
- Also not possible to solve for Space Optimisation as O(1), at best only O(k)
