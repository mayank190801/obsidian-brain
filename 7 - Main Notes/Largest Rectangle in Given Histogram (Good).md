
[[DSA]]
[[Stack and Queue DSA]]

- solved using nser and nsel (pretty cool)
https://leetcode.com/problems/largest-rectangle-in-histogram/



```java
class Solution {    
    public int largestRectangleArea(int[] heights) {
        int ans = 0;
        Deque<Integer> stack = new ArrayDeque<>();
        for(int i = 0; i <= heights.length; i++){            
            int currVal = i == heights.length ? 0 : heights[i];
            while(!stack.isEmpty() && heights[stack.peek()] > currVal){
                int prevIdx = stack.pop();
                int prevValue = heights[prevIdx];
                int prevprevIdx = stack.isEmpty() ? -1 : stack.peek();

                int currAns = prevValue * (i - prevprevIdx - 1);
                ans = Math.max(ans, currAns);
            }
            stack.push(i);
        }
        return ans;
    }
}
```