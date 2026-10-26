
[[DSA]]
[[Graph DSA]]

//Implement all of these 3 and see how they performs!!!  - totally your call!

- Either use Queue and normal traversal
- Either use DP with PQ
- Either use PQ with stops preference and then dist preference

```java
class Solution {
    public int findCheapestPrice(int n, int[][] flights, int src, int dst, int k) {
        //make a graph with flight 
        ArrayList<Pair>[] graph = new ArrayList[n];
        for(int i = 0; i < n; i++){
            graph[i] = new ArrayList<>();
        }
        for(int i = 0; i < flights.length; i++){
            int u = flights[i][0];
            int v = flights[i][1];
            int wt = flights[i][2];
            graph[u].add(new Pair(v, wt));
        }

        int[][] dist = new int[n][k + 1];
        for(int i = 0; i < n; i++){
            for(int j = 0; j <= k; j++){
                dist[i][j] = Integer.MAX_VALUE;
            }
        }        
        dist[src][0] = 0;  //for k stops
        

        PriorityQueue<Triplet> que = new PriorityQueue<>((a,b) -> Integer.compare(a.wt, b.wt));
        que.add(new Triplet(src, 0, 0));

        while(!que.isEmpty()){
            // System.out.println(que);
            Triplet curr = que.poll();
            if(curr.k == k + 1) continue;  

            for(Pair edge : graph[curr.node]){
                if(dist[edge.node][curr.k] > curr.wt + edge.wt){
                    dist[edge.node][curr.k] = curr.wt + edge.wt;                    
                    que.add(new Triplet(edge.node, dist[edge.node][curr.k], curr.k + 1));
                }             
            }
        }

        // System.out.println(Arrays.deepToString(dist));
        int ans = Integer.MAX_VALUE;
        for(int i = 0; i <= k; i++) ans = Math.min(ans, dist[dst][i]);
        return ans == Integer.MAX_VALUE ? -1 : ans;        
    }

    public class Triplet {
        int node;
        int wt;
        int k;
        Triplet(int node, int wt, int k){
            this.node = node;
            this.wt = wt;
            this.k = k;        
        }

        @Override 
        public String toString(){
            return node + " " + wt + " " + k;
        }
    }

     public class Pair {
        int node;
        int wt;        
        Pair(int node, int wt){
            this.node = node;
            this.wt = wt;            
        }

        @Override 
        public String toString(){
            return node + " " + wt;
        }
    }
}
```


