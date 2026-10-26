
2024-06-26 07:17
Status: #child 
Tags: [[data structures]] [[graphs]]

# Kosa Raju Algorithm

Big Idea 
- If first we are reaching out to everyone, then later on we will see if other nodes can reach out to us, if not, then they are not strongly connected with us - (damn real life meaning)

Use case
- It is used to find the strongly connected components

Implementation 
- First go through the graph normally and add all the element in stack
- Reverse the graph and see how many you can reach out to - those are strongly connected only

Algorithm 
```
public static int getSCC() {
        boolean[] vis = new boolean[n];
        // step 1
        Stack<Integer> order = new Stack<>();
        for (int i = 0; i < n; i++) {
            if (!vis[i]) {
                dfsScc(graph, i, vis, order);
            }
        }

        // step2
        ArrayList<Edge>[] revgraph = new ArrayList[n];
        for (int i = 0; i < n; i++) {
            revgraph[i] = new ArrayList<>();
        }
        for (int i = 0; i < n; i++) {
            for (Edge e : graph[i]) {
                revgraph[e.v].add(new Edge(i, e.wt));
            }
        }

        // STEP 3
        vis = new boolean[n];
        int scc = 0;
        while (order.size() > 0) {
            int i = order.pop();
            if (!vis[i]) {
                dfsScc(revgraph, i, vis, new Stack<>());
                scc++;
            }
        }
        return scc;
    }

```


# **References**