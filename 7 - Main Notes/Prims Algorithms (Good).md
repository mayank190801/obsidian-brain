
2024-06-29 08:26
Status: #baby 
Tags: [[data structures]] [[graphs]]

# Prims Algorithms

Big Idea  - Basically start with any vertex, and only add another vertex if it is the current lowest weighted edge in all the ones we have added in Priority Queue.

Time Complexity : 
Space Complexity : 

Implementation 
- Start with some node and all the edges touching it 
- Now pick the edge with lowest weight, and add all the edges for it to which the node has not been visited yet
- Isme sirf edge ka weight hota hai and node unvisited hona chahiye (core)

Algorithm
```
 static int spanningTree2(int V, int E, int edges[][]){
        ArrayList<Pair2>[] graph = new ArrayList[V];
        for(int i = 0; i < V; i++){
            graph[i] = new ArrayList<>();
        }

        for(int i = 0; i < E; i++){
            int[] edge = edges[i];
            int u = edge[0];
            int v = edge[1];
            int cost = edge[2];

            graph[v].add(new Pair2(u, cost));  //bi directional hoti hai?
            graph[u].add(new Pair2(v, cost));
        }

        int[] vis = new int[V];
        int cost = 0;
        PriorityQueue<Pair2> que = new PriorityQueue<>((Pair2 a, Pair2 b) -> (a.b - b.b));   //hmm

        vis[0] = 1;
        for(Pair2 edge : graph[0]){
            que.add(edge);
        }

        while(!que.isEmpty()){
            Pair2 curr = que.poll();
            if(vis[curr.a] == 1) continue; 
            vis[curr.a] = 1;
            cost += curr.b;
            for(Pair2 p : graph[curr.a]){
                if(vis[p.a] == 1) continue;
                que.add(p);
            }
        }

        return cost;
    }

    public class Pair2{
        int a;
        int b;
        Pair2(int a, int b){
            this.a = a;
            this.b = b;
        }
    }

```







# **References**