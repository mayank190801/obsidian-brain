
[[DSA]]
[[Graph DSA]]

- YOU CAN USE Queue (but it is not efficient!!1)

- using priority queue 
- sort them on the basis of current distance to reach that node 



```java
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
