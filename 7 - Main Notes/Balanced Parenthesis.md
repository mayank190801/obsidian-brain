[[DSA]]
[[Stack and Queue DSA]]

```java
class Solution {
    public boolean isValid(String s) {
        Deque<Character> stack = new ArrayDeque<>();
        char[] arr = s.toCharArray();
        for(char ch : arr){
            if(ch == '(' || ch == '[' || ch == '{'){
                stack.push(ch);
            }else{
                if(stack.isEmpty()) return false;
                char prev = stack.peek();
                if(ch == ')' && prev != '(') return false;
                if(ch == '}' && prev != '{') return false;
                if(ch == ']' && prev != '[') return false;
                stack.pop();
            }
        }
        return stack.isEmpty();        
    }
}
```
