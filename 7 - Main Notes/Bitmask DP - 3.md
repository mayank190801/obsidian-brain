
[[DP with BitMasking]]


https://codeforces.com/contest/16/problem/E

Crazy problem!!! 
1900 rated on codeforces 

basically we need the answer for set {1}, {2}, {3}
// and the comes from {1,2}, {1,3}, {1,4}

//REALLY COOL TO SOLVE THIS PROBLEM 
```java
    public static void main(String[] args) {  
        MyScanner sc = new MyScanner(); // pretty important for sure -  
        out = new PrintWriter(new BufferedOutputStream(System.out)); // dope shit output for sure  
  
        int n = sc.nextInt();  
        double[][] prob = new double[n][n];  
        for(int i = 0; i < n; i++){  
            for(int j = 0; j < n; j++){  
                prob[i][j] = sc.nextDouble();  
            }  
        }  
        Double[] dp = new Double[1 << (n + 1)];  
        for(int i = 0; i < n; i++){  
            double ans = helper(1 << i, n, prob, dp);  
            System.out.print(ans + " ");  
        }  
        System.out.println();  
        out.close();  
    }  
  
    public static double helper(int bitmask, int n, double[][] prob, Double[] dp){  
//        System.out.println(bitmask);  
        if(dp[bitmask] != null) return dp[bitmask];  
        //if we have {1 , 2}  
        int setBits = setBitsCounter(bitmask);  
        if(setBits == n) return 1.0;  //base case brother  
        int options = (setBits * (setBits + 1))/2;  
        double answer = 0;  
        for(int i = 0; i < n; i++){  
            if((bitmask & (1 << i)) == 0){  
                int nbitmask = (bitmask ^ (1 << i));  
                double probOfAddition = helper(nbitmask, n, prob, dp);  
                double probOfDeletion = 0.0;  
                for(int j = 0; j < n; j++){  
                    if((bitmask & (1 << j)) > 0){  
//                        System.out.println("WHAT THE FUCK");  
                       probOfDeletion += prob[j][i];  
                    }  
                }  
                probOfDeletion /= (double) options;  
//                System.out.println(i);  
//                System.out.println(bitmask);  
//                System.out.println(options);  
//                System.out.println(probOfAddition);  
//                System.out.println(probOfDeletion);  
                answer += (probOfAddition * probOfDeletion);  
            }  
        }  
       return dp[bitmask] = answer;  
    }  
  
    public static int setBitsCounter(int num){  
        int cnt = 0;  
        while(num != 0){  
            if((num & 1) == 1) cnt++;  
            num = num >> 1;  
        }  
        return cnt;  
    }
}
```