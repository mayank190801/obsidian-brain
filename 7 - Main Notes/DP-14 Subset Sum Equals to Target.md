[[DSA]]
[[Dynamic Programming DSA]]

https://www.naukri.com/code360/problems/subset-sum-equal-to-k_1550954?leftPanelTab=1%3Fsource%3Dyoutube&campaign=striver_dp_videos&utm_source=youtube&utm_medium=affiliate&utm_campaign=striver_dp_videos&leftPanelTabValue=SUBMISSION


- Basically recursion is either picking up or not picking up 
- And proper edge cases 
- TC - O(2^N) and O(N) auxiliary space


```
    public static boolean subsetSumToK(int n, int k, int arr[]){
        boolean[] prev = new boolean[k + 1];
        boolean[] curr = new boolean[k + 1];
        prev[0] = true;
        curr[0] = true;      
        if(arr[0] <= k) prev[arr[0]] = true;

        for(int j = 1; j < n; j++){
            for(int i = 1; i <= k; i++){
                boolean notTake = prev[i];
                boolean take = false;
                if(i - arr[j] >= 0) {
                    take = prev[i - arr[j]];
                }

                curr[i] = take || notTake;
            }
            boolean[] temp = curr;
            curr = prev;
            prev = temp;
        }
        return prev[k];
    }
```


So the above code is pretty not so advisable way of doing this thing 
- In the above code target is first then idx, so basically in tabulation format you are parsing from top to bottom rather than left to right 
- Due to this a lot of logical changes are required to not mess up the functioning of the code 

Rest edge cases are important and how to set the state of the edge cases, 
Let's solve this in normal format also once and add that baby in here 

//Recursion is pretty simple let me share that as well

```
    public static boolean recurSubset(int n, int[] arr, int left, int idx, int[][] dp){
        if(left == 0) return true;
        if(idx < 0 || left < 0) return false;
        if(dp[left][idx] != 0) return dp[left][idx] == 1 ? true : false;

        boolean pos = false;
        pos = recurSubset(n, arr, left - arr[idx], idx - 1, dp) || recurSubset(n, arr, left, idx - 1, dp);

        dp[left][idx] = pos ? 1 : -1;
        return pos;
    }
```



Actualy way of solving from left to right  (this bad boy makes the most sense)

```
public static boolean subsetSumToK(int n, int k, int arr[]){
        boolean[][] dp = new boolean[n][k + 1];
        for(int i = 0; i < n; i++){
            dp[i][0] = true;
        }
        if(arr[0] <= k) dp[0][arr[0]] = true;

        for(int i = 1; i < n; i++){
            for(int j = 1; j <= k; j++){
                boolean notTake = dp[i - 1][j];
                boolean take = false;
                if(j - arr[i] >= 0) {
                    take = dp[i - 1][j - arr[i]];
                }

                dp[i][j] = take || notTake;
            }
        }
        return dp[n - 1][k];
    }
```



SOLVED USING SINGLE ARRAY  (smart enough to sovle it )

//base cases should be handled nicely brother (that's what I genuinely feel about it!)

```java

public class Solution {
    public static boolean subsetSumToK(int n, int k, int arr[]) {
       	boolean[] dp = new boolean[k + 1]; 
		dp[0] = true;
		if(arr[0] <= k) dp[arr[0]] = true;
		for(int idx = 1; idx < n; idx++){
			for(int left = k; left >= 1; left--){  
				boolean notPick = dp[left];			
				boolean pick = false;
				if(arr[idx] <= left) pick = dp[left - arr[idx]];
				dp[left] = pick || notPick;
			}
		}
	return dp[k];
}

```