

[[DSA]]
[[Binary Search DSA]]

https://leetcode.com/problems/search-a-2d-matrix-ii/

- start from top right corner, and move left or down depending on where the answer could be present!!! (pretty dope shit )

```java
class Solution {
     public boolean searchMatrix(int[][] matrix, int target) {
        int i = 0;
        int j = matrix[0].length-1;

        int r = matrix.length;
        int c = j+1;

        while(i < r && j > -1){
            if(matrix[i][j] == target) return true;
            else if(matrix[i][j] > target){
                j--;
            }else{
                i++;
            }
        }

        return false;
    }
}
```