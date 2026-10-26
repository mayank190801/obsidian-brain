Really less intutive problem 
Similar to stack that for each we add or substract 
But isme we don't keep stack we use leftMax and rightMax and then for shorter one contribute to the answer

```java

class Solution {

    //more 2 pointers problem i need to solve for sure 
    //2 pointers 
    public int trap(int[] height) {
        int leftMax = 0;
        int rightMax = 0;
        int left = 0;
        int right = height.length - 1;
        int water = 0;
        while(left < right){            
            int lh = height[left];
            int rh = height[right];
            if(lh <= rh){
                if(leftMax > lh) water += leftMax - lh;
                leftMax = Math.max(leftMax, lh);
                left++;
            }else{
                if(rightMax > rh) water += rightMax - rh;
                rightMax = Math.max(rightMax, rh);
                right--;
            }
         
        }
        return water;        
    }
}
```
