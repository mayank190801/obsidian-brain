
Tags : [[Dynamic Programming DSA]]

- Learning Integer.ParseInt ~ Important
- Use Switch in these scenarios 
- Base cases can be handled pretty differently ~ (rather than picking up initially)

- MCM sort of DP question 
- Can be further optimised to be in tabulation form only 
- Need to learn the above technique


Time Complexity ~ O(N^3)
Space Complexity ~ O(N^2)

```java
class Solution {
     //Time Complexity ~ O(n^3)
    //Space Complexity ~ O(n^2)
    public List<Integer> diffWaysToCompute(String expression) {
        int len = expression.length();
        List<Integer>[][] dp = new ArrayList[len + 1][len + 1];
        return recursionDiffWays(expression, 0, expression.length() - 1, dp);
    }

    public List<Integer> recursionDiffWays(String expression, int i, int j, List<Integer>[][] dp){
        if(dp[i][j] != null) return dp[i][j];
        List<Integer> currAns = new ArrayList<>();
        for(int k = i; k <= j; k++){
            char curr = expression.charAt(k);
            if(curr == '+' || curr == '-' || curr == '*'){
                List<Integer> left = recursionDiffWays(expression, i, k-1, dp);
                List<Integer> right = recursionDiffWays(expression, k+1, j, dp);

                //this below way looks better
                for (Integer leftAns : left) {
                    for (Integer rightAns : right) {
                        int c = 0;
                        switch (curr){
                            case '+' :
                                c = leftAns + rightAns;
                                break;
                            case '-' :
                                c = leftAns - rightAns;
                                break;
                            case '*' :
                                c = leftAns * rightAns;
                                break;
                        }
                        currAns.add(c);
                    }
                }
            }
        }
        if(currAns.size() == 0) currAns.add(Integer.parseInt(expression.substring(i, j + 1)));
        return dp[i][j] = currAns;
    }
}
```