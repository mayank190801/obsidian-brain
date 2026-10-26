
[[DSA]]
[[Graph DSA]]

- helps you detect negative cycles as well 
- Directed Graphs required (Change undirected graph to directed graph)

- Total V - 1 iterations are required and go through all the edge
- If at Vth iteration again some change happens!!! (hence negative cycle present)
- Simple algorithm baaki toh


```java
class Solution {
    static int[] bellmanFord(int V, int[][] edges, int S) {
        // Initialize distance of all vertices as infinite.
        int[] dis = new int[V];
        int inf = 100000000;
        for (int i = 0; i < V; i++) dis[i] = 100000000;

        // initialize distance of source as 0
        dis[S] = 0;

        // Relax all edges |V| - 1 times. A simple
        // shortest path from src to any other
        // vertex can have at-most |V| - 1 edges
        // int E=edges.length;
        for (int i = 0; i < V - 1; i++) {
            for (int j = 0; j < edges.length; j++) {
                if (dis[edges[j][0]] != inf &&
                    dis[edges[j][0]] + edges[j][2] < dis[edges[j][1]])
                    dis[edges[j][1]] = dis[edges[j][0]] + edges[j][2];
            }
        }
        for (int j = 0; j < edges.length; j++) {
            if (dis[edges[j][0]] != inf &&
                dis[edges[j][0]] + edges[j][2] < dis[edges[j][1]]) {
                return new int[] {-1};
            }
        }
        return dis;
    }
}
```
