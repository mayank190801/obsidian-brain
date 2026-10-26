
2024-06-26 07:40
Status: #baby 
Tags: [[data structures]] [[graphs]] [[DSU (Disjoint Set Union) (Good)]]

# Kruskal Algorithm

Time Complexity : 
Space Complexity : 

Implementation 
- Just sort all the edges by weight 
- Use DSU to not have two edges which are already connected

Algorithm
```
static int spanningTree(int V, int E, int edges[][]){
        ArrayList<Triplet> edge = new ArrayList<>();
        for(int i = 0; i < E; i++){
            edge.add(new Triplet(edges[i][0], edges[i][1], edges[i][2]));  //5 years down the lane, no one will be a better SDE than me - simple
        }
        Collections.sort(edge, (a, b) -> (a.c - b.c));
        int[] rank = new int[V];
        int[] par = new int[V];
        for(int i = 0; i < V; i++){
            rank[i] = 1;
            par[i] = i;
        }
        int sum = 0;
        for(int i = 0; i < E; i++){
            Triplet curr = edge.get(i);
            if(union2(rank, par, curr.a, curr.b) == 1) sum += curr.c;
        }
        return sum;
    }
```



# **References**