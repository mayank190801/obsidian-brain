
[[DSA]]
[[Graph DSA]]

- Good question and good use of StringBuilder smart technique!! 

```java
class Solution {
    public int numDistinctIslands(int[][] grid) {
        Set<String> set = new HashSet<>();
        int n = grid.length;
        int m = grid[0].length;
        StringBuilder sb = new StringBuilder();
        int[][] vis = new int[n][m];
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                if(grid[i][j] == 1 && vis[i][j] != 1){
                    vis[i][j] = 1;
                    dfs(grid, i, j, sb, vis);
                    set.add(sb.toString());
                    sb.setLength(0);
                }                
            }
        }
        return set.size();
    }

    public int[][] directions = { { 0, 1 }, { 1, 0 }, { 0, -1 }, { -1, 0 } };
    public char[] move = { 'L', 'U', 'D', 'R' };

    public void dfs(int[][] grid, int x, int y, StringBuilder sb, int[][] vis) {
        int n = grid.length;
        int m = grid[0].length;
        int idx = 0;
        boolean end = true;
        for (int[] dir : directions) {
            int nx = x + dir[0];
            int ny = y + dir[1];
            if (nx >= 0 && nx < n && ny >= 0 && ny < m && grid[nx][ny] == 1 && vis[nx][ny] != 1) {            
                vis[nx][ny] = 1;
                sb.append(move[idx]);
                dfs(grid, nx, ny, sb, vis);
                end = false;
                sb.append('E');
            }
            idx++;
        }
        
    }
}

```