
learnings 
- just think greedily 
- why we are moving the shorter one inwards? 
- Because we know there is no one its right which is greater than the current left one!!!! otherwise left would have moved inwards!!! (think think think)
- We are basically bullying the shortes one to come inward because we know we can, if it would have been taller or had any taller parents, we would be getting bullied right now 
- This is greedy way and exhaustive solution for the problem 

```java
class Solution {
    //very simple two pointer logic because 
    //think about it 
    public int maxArea(int[] height) {
        int ans = 0;        
        int left = 0;
        int right = height.length - 1;
        while(left < right){
            ans = Math.max(ans, Math.min(height[left], height[right]) * (right - left));
            if(height[left] > height[right]) right--;
            else left++;            
        }
        return ans;        
    }
}
```