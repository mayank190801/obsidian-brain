
[[DSA]]
[[Tree DSA]]


- Recursive solution is pretty easy and clear 

```java
class Solution {
  //validate BST, simple as that
    public boolean isValidBST(TreeNode root) {
        return helper(root, Long.MIN_VALUE, Long.MAX_VALUE);
    }

    public boolean helper(TreeNode root, long left, long right){
        if(root == null) return true;
        if(!(root.val < right && root.val > left)) return false;
        return helper(root.left, left, root.val) && helper(root.right, root.val, right);
    }
}
```
