[[DSA]]
[[Dynamic Programming DSA]]

Let's keep these simple 

1. **Recursion** 

- f(n) = f(n - 1) + f(n - 2)
- Time Complexity - O(2^n)
- Space Complexity - O(n)

2. **Recursion + memoization** 

- Use array to store the answers for solved subproblems
- Time Complexity - O(n)
- Space Complexity - O(n) (stack) + O(n) (dp)

3.  **Tabulation** 

- Use for loop and array  
- Time Complexity - O(n)
- Space Complexity - O(n) (dp)

4. **Tabulation + space optimization** 

- Use for loop and variables 
- Time Complexity - O(n)
- Space Complexity - O(1)
