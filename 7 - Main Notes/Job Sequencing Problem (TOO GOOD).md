
[[DSA]]
[[DSU (Disjoint Set Union) (Good)]]
[[Greedy DSA]]


https://www.geeksforgeeks.org/problems/job-sequencing-problem-1587115620/1?itm_source=geeksforgeeks&itm_medium=article&itm_campaign=practice_card

- All the concepts are too good in this question!! (really loved this problem)
- First sort on the basis of profits, then deadlines 
- Then go and pick a job, and put it at the deadline array 
- Next pick the job, if the deadline array is filled at that spot, pick a spot before the deadline array 
- Now you would think finding the empty spot in the deadline array would be O(N) operation!!! 
- BUT NOOO, YOU CAN USE DSU here!! (just union two sets!!)


//Crazy problem man 


```java
class Solution {
    public ArrayList<Integer> JobSequencing(int[] id, int[] deadline, int[] profit) {
        int n = id.length;
        ArrayList<Pair> jobs = new ArrayList<>();
        for(int i = 0; i < n; i++){
            jobs.add(new Pair(deadline[i], profit[i]));
        }
        
        Collections.sort(jobs, (a, b) -> b.profit - a.profit == 0 ? a.deadline - b.deadline : b.profit - a.profit);
        DisjointSet dsu = new DisjointSet(n + 1);
        
        int totalJobs = 0;
        int totalProfit = 0;
        for(int i = 0; i < n; i++){
            Pair job = jobs.get(i);
            int parent = dsu.find(job.deadline);
            if(parent != 0){
                totalJobs++;
                totalProfit += job.profit;
                dsu.union(dsu.find(parent - 1), parent);
            }
        }    
        
        return new ArrayList<>(Arrays.asList(totalJobs, totalProfit));
    }
    
    public class DisjointSet {
        int[] par;
        DisjointSet(int size){
            this.par = new int[size];
            for(int i = 0; i < size; i++){
                par[i] = i;
            }
        }
        
        public int find(int u){
            return par[u] == u ? u : (par[u] = find(par[u]));
        }
        
        public int union(int u, int v){
            int par1 = find(u);
            int par2 = find(v);
            if(par1 == par2) return -1;
            par[par2] = par1;
            return 1;
        }
    }
    
    public class Pair {
        int deadline;
        int profit;
        Pair(int deadline, int profit){
            this.deadline = deadline;
            this.profit = profit;
        }
    }
}
```