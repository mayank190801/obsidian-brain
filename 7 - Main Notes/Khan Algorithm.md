
2024-06-25 10:25
Status: #child  
Tags: [[data structures]] [[graphs]]

# Khan Algorithm

**Space Complexity - O(V) 
Time Complexity - O(V + E)**

- It used to get the topological sorting
- Also for finding if there is a cycle in directed graphs

Implementation 
- First create an array of indegrees
- Then start from the node with 0 indegree, and go one level deeper everytime 

Algorithm

```
public static void kahnsAlgo() {
        int[] indegree = new int[n];
        for (int i = 0; i < n; i++) {
            for (Edge e : graph[i]) {
                indegree[e.v]++;
            }
        }
        Queue<Integer> que = new LinkedList<>();
        for (int i = 0; i < n; i++) {
            if (indegree[i] == 0) {
                que.add(i);
            }
        }
        List<Integer> order = new ArrayList<>();
        while (que.size() > 0) {
            int top = que.poll();
            order.add(top);
            for (Edge e : graph[top]) {
                indegree[e.v]--;
                if (indegree[e.v] == 0) {
                    que.add(e.v);
                }
            }
        }
        if (order.size() == n) {
            System.out.println(order);
        } else {
            System.out.println("Cyclic Graph");
        }
    }
```






# **References**