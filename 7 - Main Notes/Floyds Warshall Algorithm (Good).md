
[[DSA]]
[[Graph DSA]]

- Create adjacency matrix first
- Pick all the nodes once 
- And then go through all i an j combinations and make k pass through them 
- ki i se k and k se j < i j or not (check this and update this!!) - pretty simple

```java
class Solution
{
   public void shortest_distance(int[][] matrix)
    {
        int n = matrix.length;
        for(int i = 0; i < n; i++){
            for(int j = 0; j < n; j++){
                if(matrix[i][j] == -1) matrix[i][j] = Integer.MAX_VALUE;
            }
        }

        //now update this matrix itself 
	    for(int k = 0; k < n; k++){
	        for(int i = 0; i < n; i++){
	            for(int j = 0; j < n; j++){
                    if(matrix[i][k] != Integer.MAX_VALUE && matrix[k][j] != Integer.MAX_VALUE){
                        if(matrix[i][k] + matrix[k][j] < matrix[i][j]){
                            matrix[i][j] = matrix[i][k] + matrix[k][j];
                        }
                    }
                }
            }
        }

        for(int i = 0; i < n; i++){
            for(int j = 0; j < n; j++){
                if(matrix[i][j] == Integer.MAX_VALUE) matrix[i][j] = -1;
            }
        }

    }
}
```

