

[[DSA]]
[[Stack and Queue DSA]]

https://leetcode.com/problems/min-stack/description/

3 ways of solving this questions
- first one is simpy by using two stack  (best)
- second one is create a Node class and making a proper stack  (actual stack!!)
- third one is using less space and only storing one number in stack (O(n) - space only) 

```java
class MinStack {
    long min = 0;
    Deque<Long> stack;
    public MinStack() {        
        stack = new ArrayDeque<>();
    }
    
    public void push(int val) {
        if(stack.isEmpty()) {
            stack.push((long)val);
            min = (long)val;
        }else{
            if(val < min){
                stack.push(2L * (long)val - min);
                min = (long)val;
            }else{
                stack.push((long)val);
            }
        }        
    }
    
    public void pop() {
        long x = stack.pop();
        if(x < min){
            min = 2L * min - x;            
        }
    }
    
    public int top() {
        long val = stack.peek();
        return (int) (val);
    }
    
    public int getMin() {
        return (int)min;
    }
}
```

