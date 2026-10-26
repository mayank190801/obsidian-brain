
[[DSA]]
[[Tree DSA]]


```java
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if(p.val > q.val) return lowestCommonAncestor(root, q, p);
        if(root == null) return null;
        if(root.val == p.val || root.val == q.val || (root.val < q.val && root.val > p.val)) return root;
        if(root.val < q.val) return lowestCommonAncestor(root.right, p, q);
        else return lowestCommonAncestor(root.left, p, q);        
    }
}
```