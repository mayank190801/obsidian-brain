
[[Dynamic Programming DSA]]

What is bitmask??

Using numbers to store subset basically! 
- that is the core logic for this bad boi 

Like lets say 5 -  101 (so 1st bit from the right is the 1st element is present or not and so )

- add function 
- remove function 
- display function 

can be created using the concepts of bitmasking!!! (pretty darn cool I believe)



```java

Problem 1 
	- basic nxn matrix and find the least cost for jobs and people 

public int solve(int n, int[][] cost){
//using dp array for states and stuff can also solve this problem very well 
//we will come across actual leetcode bitmask problems and solve those really well 
//just keep on coding and never give up 
//learn cool concepts 

}

public int helper(int person, int bitmask, int n) {
	if(person == n) return 0;

int minimum = Integer.MAX_VALUE;
for(int i = 0; i < n; i++){
	if(bitmask & (1 << i ) > 0) {
		int ans = cost[person][i] + helper(person + 1, remove(bitmask, i), n);
}
} 

return minimum;
}

public int remove(int bitmask, int pos){
	return ~(1 << pos) & bitmask);
}

```


Travelling Salesman problem - can be easily converted to bitmask dp as well 

{1, {2,3,4,5,6,7}}
and so on other states, plus you can replace the second parameter with bitmask!! (how cool is that!!)

[[[Bitmask DP - 3]]
