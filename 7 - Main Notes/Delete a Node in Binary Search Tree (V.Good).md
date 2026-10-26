
[[DSA]]
[[Tree DSA]]

//WRITE ITERATIVE AND RECURSIVE SOLUTION FOR THIS ONE 

//Below is recusrive solution - please write the iterative solution as well
```java
class Solution {
    public TreeNode deleteNode(TreeNode root, int key) {
        if (root == null)
            return root;
        if (root.val == key) {
            if (root.left == null || root.right == null) {
                return root.left == null ? root.right : root.left;
            }
            TreeNode temp = root.right;
            while (temp.left != null)
                temp = temp.left;
            temp.left = root.left;
            return root.right;
        }
        if(root.val > key){
            root.left = deleteNode(root.left, key);
        }else{
            root.right = deleteNode(root.right, key);
        }
        return root;
    }
}

```