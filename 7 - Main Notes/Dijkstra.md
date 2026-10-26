
2024-06-25 10:09
Status: #baby 
Tags:  [[data structures]] [[graphs]]

# Dijkstra

Time/Space Complexity 
Have to think about it 

Logic 
- Start with the (source and current distance), and traverse all the edges
- If you are able to reach a node with better distance than stored! 
- Then simply update the dist, and store the new node and better distance in a pair (in priority queue)

Algorithm 
```
static int[] dijkstra(int V, ArrayList<ArrayList<ArrayList<Integer>>> adj, int S)
    {
        int[] dist = new int[V];
        Arrays.fill(dist, Integer.MAX_VALUE);
        dist[S] = 0;

        PriorityQueue<Pair> pq = new PriorityQueue<Pair>((a,b) -> a.b - b.b);
        pq.add(new Pair(S, 0));

        while(!pq.isEmpty()){
            Pair curr = pq.poll();
            for(ArrayList<Integer> edge : adj.get(curr.a)){
                if(curr.b + edge.get(1) < dist[edge.get(0)]){
                    dist[edge.get(0)] = curr.b + edge.get(1);
                    pq.add(new Pair(edge.get(0), dist[edge.get(0)]));
                }
            }
        }

        return dist;
    }
```


# **References**
