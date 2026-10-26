[[DSA]]
[[Dynamic Programming DSA]]

https://www.naukri.com/code360/problems/longest-increasing-subsequence_630459?source=youtube&campaign=striver_dp_videos&utm_source=youtube&utm_medium=affiliate&utm_campaign=striver_dp_videos&leftPanelTabValue=SUBMISSION

- Ways 
- You can start with recursion, then memoization 
- Then O(N^2) solution with O(N^2) space dp 
- Then O(N^2) solution with O(N) space
- Finally O(NlongN) with O(N) space (crazy)

- The binary search logic is insane and that is just out of my brain 




```java

public static int longestIncreasingSubsequence(int arr[]) {
        List<Integer> list = new ArrayList<>();
        for(int i : arr){
            int idx = lowerBound(list, i);
           
            if(idx == list.size() - 1){
                list.add(i);
            }else{
                if(list.get(idx + 1) > i){
                    list.set(idx + 1, i);
                }
            }
        };;d
        return list.size();
    }

    public static int lowerBound(List<Integer> list, int val){
        int ans = -1;
        int low = 0;
        int high = list.size() - 1;
        while(low <= high){
            int curr = (low + high)/2;

            if(list.get(curr) < val){
                ans = Math.max(ans, curr);
                low = curr + 1;
            }else{
                high = curr - 1;
            }
        }
        return ans;
    }
```


```java
import java.util.*;

public class Solution {
	public static int longestIncreasingSubsequence(int arr[]) {
        List<Integer> list = new ArrayList<>();
        for(int i : arr){
            int idx = lowerBound(list, i);
           
            if(idx == list.size() - 1){
                list.add(i);
            }else{
                if(list.get(idx + 1) > i){
                    list.set(idx + 1, i);
                }
            }
        }
        return list.size();
    }

    public static int lowerBound(List<Integer> list, int val){
        int ans = -1;
        int low = 0;
        int high = list.size() - 1;
        while(low <= high){
            int curr = (low + high)/2;

            if(list.get(curr) < val){
                ans = Math.max(ans, curr);
                low = curr + 1;
            }else{
                high = curr - 1;
            }
        }
        return ans;
    }
}
```