
[[DSA]]
[[Tree DSA]]


one way 
```java
class Solution {

    Map<TreeNode, TreeNode> mapToParent;

    public List<Integer> distanceK(TreeNode root, TreeNode target, int k) {
        mapToParent = new HashMap<>();
        createMapToParent(root, null);
        int[] vis = new int[501];
        ArrayDeque<TreeNode> que = new ArrayDeque<>();
        que.add(target);
        vis[target.val] = 1;
        while (!que.isEmpty()) {
            int size = que.size();
            if (k == 0)
                break;
            k--;
            while (size-- > 0) {
                TreeNode curr = que.poll();
                if (curr.left != null && vis[curr.left.val] != 1) {
                    vis[curr.left.val] = 1;
                    que.add(curr.left);
                }

                if (curr.right != null && vis[curr.right.val] != 1) {
                    vis[curr.right.val] = 1;
                    que.add(curr.right);
                }

                if (mapToParent.get(curr) != null) {
                    TreeNode par = mapToParent.get(curr);
                    if (vis[par.val] != 1) {
                        vis[par.val] = 1;
                        que.add(par);
                    }
                }
            }
        }

        List<Integer> ans = new ArrayList<>();
        while (!que.isEmpty()) {
            ans.add(que.poll().val);
        }
        return ans;
    }

    public void createMapToParent(TreeNode root, TreeNode parent) {
        if (root == null)
            return;
        if (parent != null)
            mapToParent.put(root, parent);
        createMapToParent(root.left, root);
        createMapToParent(root.right, root);
    }
}}
```




hardcore way of solving with recursion!!! insane brother - have to go in deeper mode to solve this brother
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 * int val;
 * TreeNode left;
 * TreeNode right;
 * TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    List<Integer> ans;

    //some question in tree concept are just fuck tards not gonna lie brother
    //like thsi
    public List<Integer> distanceK(TreeNode root, TreeNode target, int k) {
        ans = new ArrayList<>();
        helper(root, target, k, false, 0);
        return ans;
    }

    public int helper(TreeNode root, TreeNode target, int k, boolean found, int dist) {
        if (root == null)
            return -1;

        //perfect person
        if (root.val == target.val) {
            if(k == 0) ans.add(root.val);
            helper(root.right, target, k, true, 1);
            helper(root.left, target, k, true, 1);
            return 1;
        }

        if (found) {
            if (k == dist)
                ans.add(root.val);
            else {
                helper(root.left, target, k, found, dist + 1);
                helper(root.right, target, k, found, dist + 1);
            }
        } else {
            int left = helper(root.left, target, k, found, dist);
            int right = helper(root.right, target, k, found, dist);

            if (left != -1) {
                if (left == k)
                    ans.add(root.val);
                else {
                    helper(root.right, target, k, true, left + 1);
                    return left + 1;
                }
            }

            if (right != -1) {
                if (right == k)
                    ans.add(root.val);
                else {
                    helper(root.left, target, k, true, right + 1);
                    return right + 1;
                }
            }

        }

        return -1;
    }
}
```