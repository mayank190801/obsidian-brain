
[[DSA]]
[[Graph DSA]]

- Using topo sort ( but what is the benefit ?)
- You can solve it in O(V + E) , otherwise it would have taken your higher complexity !!

```java
class Solution {
    
    public class Edge {
        int node;
        int weight;
        Edge(int node, int weight){
            this.node = node;
            this.weight = weight;
        }
    }
    
    public int[] shortestPath(int V, int E, int[][] edges) {
        //indegree 
        int[] indegree = new int[V];
        ArrayList<Edge>[] graph = new ArrayList[V];
        for(int i = 0; i < V; i++) graph[i] = new ArrayList<>();
        for(int i = 0; i < edges.length; i++){
            int u = edges[i][0];
            int v = edges[i][1];
            int weight = edges[i][2];
            graph[u].add(new Edge(v, weight));
            indegree[v]++;
        }
        
        int[] dist = new int[V];
        Arrays.fill(dist, Integer.MAX_VALUE);   //in the end replace it
        dist[0] = 0;
        
        Queue<Integer> que = new ArrayDeque<>();
        for(int i = 0; i < V; i++){
            if(indegree[i] == 0) que.add(i);
        }
        
        while(!que.isEmpty()){
            int curr = que.poll();
            for(Edge edge : graph[curr]){
                indegree[edge.node]--;
                if(indegree[edge.node] == 0) que.add(edge.node);
                if(dist[curr] != Integer.MAX_VALUE && dist[edge.node] > edge.weight + dist[curr]){
                    dist[edge.node] = dist[curr] + edge.weight;
                }
            }
        }
        
        for(int i = 0; i < V; i++){
            if(dist[i] == Integer.MAX_VALUE) dist[i] = -1;
        }  
        return dist;
    }
}
```
