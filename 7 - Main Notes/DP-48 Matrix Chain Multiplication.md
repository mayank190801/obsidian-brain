[[DSA]]
[[Dynamic Programming DSA]]

https://www.naukri.com/code360/problems/matrix-chain-multiplication_975344?source=youtube&campaign=striver_dp_videos&utm_source=youtube&utm_medium=affiliate&utm_campaign=striver_dp_videos&leftPanelTabValue=SUBMISSION

- Basically cut these arrays into different parts, and solve for those parts 
- Do practise this problem, it sets up the base for future questions 

- MCM with memoization 
```java
    //TC - O(N*N) * O(N) -> O(N^3)
    //SC - O(N*N) + O(N) -> O(N^2)
    public static int matrixMultiplication(int[] arr , int N) {
        int[][] dp = new int[N + 1][N + 1];
        for(int i = 0; i <= N; i++){
            for(int j = 0; j <= N; j++){
                dp[i][j] = -1;
            }
        }
        return helperMCM(arr, N, 0, N-1, dp);
    }

    public static int helperMCM(int[] arr, int N, int i, int j, int[][] dp){
        if(j - i <= 1) return 0;
        if(dp[i][j] != -1) return dp[i][j];
        int minAns = Integer.MAX_VALUE;
        for(int k = i; k < j - 1; k++){   // i to j - 1
            int left = helperMCM(arr, N, i, k + 1, dp);
            int right = helperMCM(arr, N, k + 1, j, dp);
            int ans = arr[i] * arr[k + 1] * arr[j];
            minAns = Math.min(left + right + ans, minAns);
        }
        return dp[i][j] = minAns;
    }
```


Tabulation (Bottoms up Approach)
```java
	//TC - O(N*3)
	//SC - O(N*2)
    public static int matrixMultiplication(int[] arr, int N) {
        int[][] dp = new int[N + 1][N + 1];
        int gap = 1;
        while(gap++ < N){
            for(int i = 0; i + gap <= N - 1; i++){
                int minAns = Integer.MAX_VALUE;
                for (int k = i; k < i + gap - 1; k++) {
                    int ans = arr[i] * arr[k + 1] * arr[i + gap];
                    minAns = Math.min(dp[i][k + 1] + dp[k + 1][i + gap] + ans, minAns);
                }
                dp[i][i + gap] = minAns;
            }
        }
        return dp[0][N - 1];
    }
```