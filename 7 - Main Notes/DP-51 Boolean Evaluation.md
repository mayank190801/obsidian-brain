[[DSA]]
[[Dynamic Programming DSA]]

https://www.naukri.com/code360/problems/problem-name-boolean-evaluation_1214650?source=youtube&campaign=striver_dp_videos&utm_source=youtube&utm_medium=affiliate&utm_campaign=striver_dp_videos&leftPanelTabValue=SUBMISSION

Tabulation form? 

Best memoized solution
```java
public static int evaluateExp(String exp) {  
    char[] expression = exp.toCharArray();  
    int size = expression.length;  
    int[][][] dp = new int[size + 1][size + 1][2];  
    for(int i = 0; i <= size; i++){  
        for(int j = 0; j <= size; j++){  
            for(int k = 0; k < 2; k++){  
                dp[i][j][k] = -1;  
            }  
        }  
    }  
    return helperExp(expression, 0, expression.length-1, true, dp);  
}  
  
public static int helperExp(char[] expression, int start, int end, boolean type, int[][][] dp){  
    if(dp[start][end][type ? 0 : 1] != -1) return dp[start][end][type ? 0 : 1];  
    if(start == end) {  //base case first of all  
        if(type && (expression[start] == 'T')) return 1;  
        if(!type && (expression[start] == 'F')) return 1;  
        return 0;  
    }  
    int answer = 0;  
    int mod = 1000000007;  
    for(int i = start + 1; i < end; i+=2){  
        char ch = expression[i];  
        int leftTrue = helperExp(expression, start, i - 1, true);  
        int leftFalse = helperExp(expression, start, i - 1, false);  
        int rightTrue = helperExp(expression, i + 1, end, true);  
        int rightFalse = helperExp(expression, i + 1, end, false);  
  
        if(ch == '|'){  
            if(type){  
                answer += ((leftFalse * rightTrue) + (leftTrue * rightTrue) + (leftTrue * rightFalse));  
            }else{  
                answer += leftFalse * rightFalse;  
            }  
        }else if(ch == '&'){  
            if(type){  
                answer += leftTrue * rightTrue;  
            }else{  
                answer += (leftFalse * rightTrue) + (leftFalse * rightFalse) + (leftTrue * rightFalse);  
            }  
        }else{  
            if(type){  
                answer += (leftTrue * rightFalse) + (leftFalse * rightTrue);  
            }else{  
                answer += (leftFalse * rightFalse) + (leftTrue * rightTrue);  
            }  
        }  
    }  
    return dp[start][end][type ? 0 : 1] = answer;  
}
```