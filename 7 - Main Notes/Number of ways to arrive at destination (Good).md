
[[DSA]]
[[Graph DSA]]

- Dijkstra + ways counter array (pretty cool)


```java
  class Pair{
    long first;
    long second;
    public Pair(long dis,long node){
        this.first=dis;
        this.second=node;
    }
}
class Solution {
   public int countPaths(int n, int[][] roads) {
        ArrayList<ArrayList<Pair>> al = new ArrayList<>();
        for(int i=0;i<n;i++){
            al.add(new ArrayList<>());
        }
        for(int x[]:roads){
            al.get(x[0]).add(new Pair(x[1],x[2]));
            al.get(x[1]).add(new Pair(x[0],x[2]));
        }
        PriorityQueue<Pair> pq = new PriorityQueue<>((a,b) -> Long.compare(a.second, b.second));
        long dist[]=new long[n];
        long ways[]=new long[n];
        for(int i=0;i<n;i++){
            dist[i]=Long.MAX_VALUE;
            ways[i]=0;
        }
        dist[0]=0;
        ways[0]=1;
        pq.add(new Pair(0,0));
        int mod = (int)(1e9+7);
        while(!pq.isEmpty()){
            Pair temp = pq.poll();
            long dis = temp.second;
            int node = (int)(temp.first);
            for(Pair it : al.get(node)){
                int adjnode = (int)it.first;
                long dw = it.second;
                if(dis+dw<dist[adjnode]){
                    dist[adjnode]=dis+dw;
                    pq.add(new Pair(adjnode,dis+dw));
                    ways[adjnode]=ways[node];
                }else if(dis+dw == dist[adjnode]){
                    ways[adjnode]= (ways[adjnode]+ways[node])%mod;
                }
            }
        }
        return (int)(ways[n-1]%mod);
    }
}
```