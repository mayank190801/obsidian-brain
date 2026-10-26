
[[DSA]]
[[Tree DSA]]

https://leetcode.com/problems/binary-tree-maximum-path-sum/


```java

class Solution {
    int ans = Integer.MIN_VALUE;

    public int maxPathSum(TreeNode root) {
        ans = Integer.MIN_VALUE;
        helper(root);
        return ans;
    }

    public int helper(TreeNode root) {
        if (root == null)
            return 0;

        int lh = helper(root.left);
        int rh = helper(root.right);
        ans = Math.max(lh + rh + root.val, ans);

        return Math.max(0, Math.max(root.val + lh, root.val + rh));
    }
}

```
