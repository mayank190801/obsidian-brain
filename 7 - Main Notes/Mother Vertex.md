
2024-06-25 14:12
Status: #baby 
Tags:  [[data structures]] [[graphs]]

# Mother Vertex

Any vertice from which we can reach all other vertices! 

Idea 
- The last mv we get, have the potential to be mother vertex, but unsure since cases exist where it is not possible, hence check it once again.
- Possible to have multiple mother vertex (find them using strongly connected components)

Algorithm
```
 public static int motherVertex() {
        boolean[] vis = new boolean[n];
        int mv = -1;

        for (int i = 0; i < n; i++) {
            if (!vis[i]) {
                dfsMV(vis, i);
                mv = i;
            }
        }
        vis = new boolean[n];
        dfsMV(vis, mv);
        for (int i = 0; i < n; i++) {
            if (!vis[i]) {
                return -1;
            }
        }
        return mv;
    }
```









# **References**