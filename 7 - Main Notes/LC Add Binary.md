[[DSA]]
[[Bit Manipulation DSA]]

https://leetcode.com/problems/add-binary/

```java
class Solution {
    public String addBinary(String a, String b) {
        StringBuilder ans = new StringBuilder();        
        int carry = 0;
        int aidx = a.length() - 1;
        int bidx = b.length() - 1;    
        while(aidx >= 0 || bidx >= 0){
            int abit = aidx >= 0 ? a.charAt(aidx) - '0' : 0;
            int bbit = bidx >= 0 ? b.charAt(bidx) - '0' : 0;
            int sum = abit + bbit + carry;
            ans.append(sum%2 == 0 ? 0 : 1);
            carry = sum > 1 ? 1 : 0;
            aidx--;
            bidx--;
        }
        if(carry > 0) ans.append('1');
        return ans.reverse().toString();
    }
}
```