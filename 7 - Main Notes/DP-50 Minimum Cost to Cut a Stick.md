[[DSA]]
[[Dynamic Programming DSA]]

https://leetcode.com/problems/minimum-cost-to-cut-a-stick/description/


- I basically solved it by taking i and j as the entire length (which was not optimal) also I did take entire cuts at each i and j (another stupid thing ) 

- optmised solution is basically sorting the cuts and using them as i , j  (that way you can use dp and ignore usage of treeSet pretty nicely)

Best DP Tabulation solution
```java
	public int minCost(int n, int[] cuts) {
        ArrayList<Integer> cutsList = new ArrayList<>();
        cutsList.add(0);
        Arrays.sort(cuts);
        for (int cut : cuts) cutsList.add(cut);
        cutsList.add(n);
        int size = cutsList.size();
        int[][] dp = new int[size][size];
        for (int start = size - 2; start >= 0; start--) {
            for (int end = start + 2; end < size; end++) {
                int minimum = Integer.MAX_VALUE;
                for (int i = start + 1; i < end; i++) {
                    int leftSubProblem = dp[start][i];
                    int rightSubProblem = dp[i][end];
                    int currAns = leftSubProblem + rightSubProblem + (cutsList.get(end) - cutsList.get(start));
                    minimum = Math.min(currAns, minimum);
                }
                dp[start][end] = minimum;

            }
        }
        return dp[0][size - 1];
    }
```

Recurrence Solution with Using i j as cuts array 
```java
	public int minCost(int n, int[] cuts) {
        ArrayList<Integer> cutsList = new ArrayList<>();
        cutsList.add(0);
        Arrays.sort(cuts);
        for (int cut : cuts) cutsList.add(cut);
        cutsList.add(n);
        int size = cutsList.size();
        int[][] dp = new int[size + 1][size + 1];
        for (int i = 0; i <= size; i++) {
            for (int j = 0; j <= size; j++) {
                dp[i][j] = -1;
            }
        }
        return minRecur(cutsList, 0, size - 1, dp);
    }

    public int minRecur(ArrayList<Integer> cutsList, int start, int end, int[][] dp) {
        if (dp[start][end] != -1) return dp[start][end];
        int minimum = Integer.MAX_VALUE;
        for (int i = start + 1; i < end; i++) {
            int leftSubProblem = minRecur(cutsList, start, i, dp);
            int rightSubProblem = minRecur(cutsList, i, end, dp);
            int currAns = leftSubProblem + rightSubProblem + (cutsList.get(end) - cutsList.get(start));
            minimum = Math.min(currAns, minimum);
        }
        return dp[start][end] = (minimum == Integer.MAX_VALUE ? 0 : minimum);
    }

```

Start Solution
```java 
class Solution {
    //badly unoptimised solution
    public int minCost(int n, int[] cuts) {
        TreeMap<Pair, Integer> map = new TreeMap<>((a, b) -> a.a - b.a == 0 ? a.b - b.b : a.a - b.a);
        return helperMinCost(n, cuts, 0, n, map);
    }

    public int helperMinCost(int n, int[] cuts, int start, int end, TreeMap<Pair, Integer> map){
        if(map.containsKey(new Pair(start, end))) return map.get(new Pair(start, end));
        int min = Integer.MAX_VALUE;
        for(int i = 0; i < cuts.length; i++){
            if(cuts[i] > start && cuts[i] < end){
                int left = helperMinCost(n, cuts, start, cuts[i], map);
                int right = helperMinCost(n, cuts, cuts[i], end, map);
                int ans = left + right + (end - start);
                min = Math.min(ans, min);
            }
        }
        map.put(new Pair(start, end), min == Integer.MAX_VALUE ? 0 : min);
        return map.get(new Pair(start, end));
    }

    public class Pair {
        int a;
        int b;
        
        Pair(int a, int b) {
            this.a = a;
            this.b = b;
        }
    }
}
```