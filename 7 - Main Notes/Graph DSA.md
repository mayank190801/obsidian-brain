
 [[DSA]]


#### LC Practise
(Good usage of int[] and List for Pair replacement - good way of doing things)
https://leetcode.com/problems/minimum-cost-of-a-path-with-special-roads/submissions/1512414794/?envType=problem-list-v2&envId=graph

(Good confusing question, can be solved in O(n^2) rather than O(n^3))
https://leetcode.com/problems/count-the-number-of-houses-at-a-certain-distance-i/description/?envType=problem-list-v2&envId=graph


#### Core Algorithms
[[Dijkstra]]
[[Khan Algorithm]] 
[[Mother Vertex]]
[[Kosa Raju Algorithm]]
[[DSU (Disjoint Set Union) (Good)]]
[[Prims Algorithms (Good)]]
Floyd Warshal
Kruskal Algorithm
BellMan Ford Algorithm

#### Representation
```java
ArrayList<Integer>[] graph = new ArrayList[n];
for(int i= 0; i < n; i++) graph[i] = new ArrayList<>();
graph[u].add(v);
graph[v].add(u);
```

#### Problems
BFS Algo (using queue)                   TC - O(V + E)
DFS Algo (using stack, recursion)  TC - O(V + E)
Number of provinces (simple bfs/dfs)
Number of islands 
Flood Fill Algorithms
[[Rotting Oranges (GOOD) (multi bfs)]]
01 matrix (multi bfs)
Cycle in undirected graph (bfs, dfs, union)
Surround Regions (Start DFS/BFS from boundary)
Number of enclaves (same as above) 
[[Number of distinct islands (GOOD)]]
Bipartite Graph https://leetcode.com/problems/is-graph-bipartite/description/ (bfs, dfs) 
[[Cycle in directed graph (Good)]]
Eventual States (dfs/ bfs (khan algo))
Topological Sorting (using dfs, using bfs (khan algo))
Alien Dictionary (GOOD)
[[Shortest Path in DAG (Good)]]
Shortest Path in Undirected Graph Having unit distance (basic bfs)
Word Ladder - I  (Simple BFS)
Word Ladder - 2 (create a queue with the linked list - crazy complexity)
[[Dijkstras Algorithm (Good)]]   TC - O(E log V) - Not possible to use for Negative Weights
Shortest Path in Weighted Undirected Graph (create a parent array and use Dijkstra)
Shortest Distance in a binary maze 
Path With Minimum Effort
[[Cheapest Flights Within K Stops (Good)]]
Minimum Multiplications To reach end
[[Number of ways to arrive at destination (Good)]]
[[BellMan Ford Algorithm (Good)]] TC - O(V E)  (takes more time than Dijkstra)
[[Floyds Warshall Algorithm (Good)]] TC - O (V^3)
City with the smallest number of neighbours at threshold distance (using above)
[[Prims Algorithms (Good)]] TC - O((V + E) log E) - (in dense E ~ V^2 and sparse E ~ V)
[[DSU (Disjoint Set Union) (Good)]] TC - O(4 x alpha) SC - O(N)
Kruskal Algo  (Use Dsu and sort the edges in sorted order (simple))
Number of provinces  (Find number of unique parents)
Connecting the graph (Count number of extra edges - union returns -1)
[[Job Sequencing Problem (TOO GOOD)]]















