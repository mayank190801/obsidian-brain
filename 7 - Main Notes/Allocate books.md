[[DSA]]
[[Binary Search DSA]]

https://www.naukri.com/code360/problems/allocate-books_1090540?leftPanelTabValue=PROBLEM


- Really cool edge case for -1 condition 
- Otherwise pretty simple 

```java
import java.util.ArrayList;
public class Solution {
    public static int findPages(ArrayList<Integer> arr, int n, int m) {
        if(n < m) return -1;
        int low = 0;
        int high = Integer.MAX_VALUE;
        int ans = Integer.MAX_VALUE;

        while(low <= high){
            int mid = low + (high - low)/2;
            if(possible(arr, n, m, mid)){
                ans = mid;
                high = mid - 1;
            }else{
                low = mid + 1;
            }
        }        
        return ans;
    }

    public static boolean possible(ArrayList<Integer> arr, int n, int m, int pages){        
        int total = 0;
        for(int i = 0; i < arr.size(); i++){
            int page = arr.get(i);
            if(page > pages) return false;
            if(page + total <= pages){
                total += page;
            }else{
                m--;
                if(m == 0) return false;
                total = page;
            }
        }
        return true;
    }
}
```