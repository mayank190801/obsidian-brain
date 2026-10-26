
[[DSA]]
[[Tree DSA]]

- using stack and O(H) space
- Pop and add left of right element, otherwise keep on going 

```java
class BSTIterator {

    Deque<TreeNode> stack;

    public BSTIterator(TreeNode root) {
        stack = new ArrayDeque<>();
        TreeNode curr = root;
        while (curr != null) {
            stack.push(curr);
            curr = curr.left;
        }
    }

    public int next() {
        TreeNode top = stack.pop();
        TreeNode node = top.right;
        while (node != null) {
            stack.push(node);
            node = node.left;
        }
        return top.val;
    }

    public boolean hasNext() {
        return !stack.isEmpty();
    }
}
```



