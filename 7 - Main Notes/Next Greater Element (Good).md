
[[DSA]]
[[Stack and Queue DSA]]


Best strategy for this!!!
- if for the right next greater you are finding
- start from the right and create a stack
- remove all small, if empty -1 otherwise the peek element is nger


```java
class Solution {    
    //if for the right next greater you are finding 
    //start from the right and create a stack 
    //remove all small, if empty -1 otherwise the peek element is nger
    public int[] nextGreaterElement(int[] nums1, int[] nums2) {    
        int n = nums1.length;
        int m = nums2.length; 
        int[] nger = new int[m];
        Map<Integer, Integer> map = new HashMap<>();
        Deque<Integer> st = new ArrayDeque<>();                
        for(int i = m - 1; i >= 0; i--){
            int ele = nums2[i];            
            while(!st.isEmpty() && st.peek() < ele) st.pop();
            if(st.isEmpty()){
                nger[i] = -1;                
                map.put(ele, -1);
            } else {
                nger[i] = st.peek();               
                map.put(ele, st.peek());
            }
            st.push(ele);
        }        
        int[] ans = new int[n];
        for(int i = 0; i < n; i++){
            ans[i] = map.get(nums1[i]);
        }
        return ans;
    }
}
```