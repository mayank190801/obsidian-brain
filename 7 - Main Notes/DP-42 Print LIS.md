[[DSA]]
[[Dynamic Programming DSA]]

- Simple use the O(N^2) approach of finding LIS 
- Create one more 1D dp which stores the best idx which helped in the creation of the current index answer
- Now backtrack from the index with the largest LIS

~ Pretty simple 