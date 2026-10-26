[[DSA]]
[[Dynamic Programming DSA]]

Problem Link - 

So I basically over-complicated the question by multiple fold 
What I did 

int one = recursion(nums, idx - 2) + nums.get(idx);  
int second = recursion(nums, idx - 3) + nums.get(idx - 1);
return Math.max(one, two)

Where as actual would be 

int one = recursion(idx - 2) + nums.get(idx)
int two = recursion(idx - 1)
return Math.max(one, two)

-- Important part was to know how subsequence are find out and etc, practise more subsequence questions for this topic

//After this 
//Memoization
//Tabulation 
//Space optimization with around 2 variables 

Best Soln
Time Complex - O(N)
Space Complex - O(1)



