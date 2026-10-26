```java
class Solution {
    public boolean isPalindrome(String s) {            
        int l = 0;
        int r = s.length() - 1;
        while(l < r){
            char lc = s.charAt(l);
            char rc = s.charAt(r);        
            if(!Character.isLetterOrDigit(lc)) l++;
            else if (!Character.isLetterOrDigit(rc)) r--;
            else if (Character.toLowerCase(lc) != Character.toLowerCase(rc)) {
                return false;
            }else {
                l++;
                r--;        
            }        
        }
        return true;        
    }
}
```			

Some improvements like - while loop usage rather than if else could have been better

Learnings 
- Character.IsLetterOrDigit()
- Character.toLowerCase()