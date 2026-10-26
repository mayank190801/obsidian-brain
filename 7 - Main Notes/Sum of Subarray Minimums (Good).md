

[[DSA]]
[[Stack and Queue DSA]]


- Great question no doubt 
- Use nsel and nser concepts to solve it 

//having mod_mul and mod_add really helps though!!

My Raw Solution
```java
class Solution {    
    //pretty dope question for real!
    long mod = 1_000_000_007L;
    public int sumSubarrayMins(int[] arr) {
        Deque<Integer> st = new ArrayDeque<>();
        long ans = 0;        
        int n = arr.length;
        for(int i = 0; i <= n; i++){
            int val = i == n ? Integer.MIN_VALUE : arr[i];
            while(!st.isEmpty() && arr[st.peek()] >= val){
                long prevIdx = st.pop();
                long prevprevIdx = st.isEmpty() ? -1 : st.peek();                
                long rem = mod_mul(prevIdx - prevprevIdx, i - prevIdx);
                rem = mod_mul(rem, arr[(int)prevIdx]);                
                ans = mod_add(ans, rem);                        
            }
            st.push(i);
        }
        return (int)ans;        
    }

    public long mod_add(long a, long b){
        return (a%mod + b%mod)%mod;
    }

    public long mod_mul(long a, long b){
        return ((a%mod) * (b%mod)) %mod;
    }
}

```