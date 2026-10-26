
[[DSA]]
[[Tree DSA]]


- requires a lot of brain power to solve this one b
- using binary search (next time solve it if you come here)


```java
class Solution {
    public int countNodes(TreeNode root) {
        int h = height(root) - 1;
        int min = 1;
        int max = 1 << h;
        int val = 1 << h;

        System.out.println(min + " " + max + " " + h);

        while (min <= max) {
            int mid = (min + max) / 2;
            if (exist(root, 1, val, mid, 0, h)) {
                min = mid + 1;
            } else {
                max = mid - 1;
            }
        }

        int ans = 0;
        for(int i = 0; i < h; i++){
            ans += (1 << i);
        }
        ans += min - 1;
        return ans;
    }

    public boolean exist(TreeNode root, int min, int max, int find, int height, int level) {
        if (root == null) {
            return height > level;
        }

        int mid = (min + max) / 2;
        if (find > mid) {
            return exist(root.right, mid + 1, max, find, height + 1, level);
        } else {
            return exist(root.left, min, mid, find, height + 1, level);
        }
    }

    public int height(TreeNode root) {
        if (root == null)
            return 0;
        return 1 + height(root.left);
    }
}
```