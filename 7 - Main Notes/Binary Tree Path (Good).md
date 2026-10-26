

[[DSA]]
[[Tree DSA]]

- Good learning question for string builder concept I believe 
- Let's go through this and see how it goes brother 

```java
class Solution {
    //using a better and faster approach I gues
    //guess what there is one more brilliant approach which takes this to 0ms
    private List<String> ans;
    public List<String> binaryTreePaths(TreeNode root) {
        ans = new ArrayList<>();
        helper(root, new StringBuilder());
        return ans;
    }

    public void helper(TreeNode root, StringBuilder sb){
        if(root == null) return;
        int len = sb.length();
        sb.append(root.val);
        if(root.left == null && root.right == null){            
            ans.add(sb.toString());    
        }        
        sb.append("->");
        helper(root.left, sb);
        helper(root.right, sb);        
        sb.setLength(len);
    }
}
```