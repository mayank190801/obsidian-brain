[[DSA]]
[[Dynamic Programming DSA]]

[Distinct Subsequences - Naukri Code 360](https://www.naukri.com/code360/problems/subsequence-counting_3755256?source=youtube&campaign=striver_dp_videos&utm_source=youtube&utm_medium=affiliate&utm_campaign=striver_dp_videos&leftPanelTabValue=SUBMISSION)

```
public static int distinctSubsequences(String str, String sub) {  
    int n = str.length();  
    int m = sub.length();  
    int modulo = 1_000_000_007;  
    //reducing the space should be very brother  
    int[] curr = new int[m + 1];  
    //base case  
    curr[0] = 1;  
    for(int i = 1; i <= n; i++){  
        for(int j = m; j >= 1; j--){  
            if(str.charAt(i - 1) == sub.charAt(j - 1)){  
                curr[j] = (curr[j - 1] + curr[j]) % modulo;  
            }else{  
                curr[j] = curr[j];  
            }  
        }  
    }  
    return curr[m];  
}
```

This question is actually brilliant and extremely hard to solve 

- So what we have learned in this one 
- That when you will be converting it to tabulation in some world, you would want to solve from i = 0 to i < n right? 
- So always think about making the answer from n - 1, m - 1
- The logic is just like subsequence we have been solving till now, if same character then send the answer in both direction, if not then only one direction 
- Pretty simple edge cases 

SUper interesting at Space Optimisation 
- 1D 2 arrays is pretty simple, just prev[0] = curr[0] = 1
- But what about only 1 1D array ---- See how we are making the answer, and simply change the way we are traversing the question !!!! 

CRAZY QUESTION --- loved it 

