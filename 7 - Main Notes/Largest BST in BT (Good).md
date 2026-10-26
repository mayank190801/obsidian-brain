
[[DSA]]
[[Tree DSA]]

https://www.geeksforgeeks.org/largest-bst-binary-tree-set-2/


- Shorter and better solution, just return a triplet from the base level and then solve this problem!! (pretty cool if you ask me)

```java
class Solution {
    
    int ans = 0;
    int largestBSTSubtree(TreeNode root)
    {
        helper(root);
        return ans;
    }
    
    Triplet helper(TreeNode curr){
        if(curr == null) return new Triplet(0, Integer.MAX_VALUE, Integer.MIN_VALUE);
        Triplet leftNode = helper(curr.left);
        Triplet rightNode = helper(curr.right);
        if(leftNode.size == -1 || rightNode.size == -1) return new Triplet(-1, -1, -1);
        if(leftNode.high < curr.val && curr.val < rightNode.low){
            int csize = 1 + leftNode.size + rightNode.size;
            ans = Math.max(ans, csize);
            return new Triplet(csize, Math.min(leftNode.low, curr.val), Math.max(rightNode.high, curr.val));
        }
        return new Triplet(-1, -1, -1);
    }
    
    class Triplet {
        int size;
        int low;
        int high;
        
        Triplet(int size, int low, int high){
            this.size = size;
            this.low = low;
            this.high = high;
        }
    }

}
```




one way of coding this bad boy
```java
class Solution {
    int ans = 0;

    public int largestBSTSubtree(TreeNode root) {
        ans = 1;
        if (root == null)
            return 0;
        helper(root);
        // System.out.println("hello?");
        return ans;
    }

    public Triplet helper(TreeNode root) {
        if (root.left == null && root.right == null) {            
            return new Triplet(root.val, root.val, 1);
        }
        boolean check = true;
        int min = root.val;
        int max = root.val;
        int size = 1;

        // System.out.println(root.val);
        /// a lot of uncessary code is present here, insane annoying 
        //never return null, return something brother!! (you have bad code brother)
        if (root.left != null) {
            Triplet left = helper(root.left);
            if (left.c == -1 || left.b >= root.val)
                check = false;
            min = left.a;
            size += left.c;
        }
        if (root.right != null) {
            Triplet right = helper(root.right);
            if (right.c == -1 || right.a <= root.val)
                check = false;
            size += right.c;
            max = right.b;
        }
        
        if(check == false) return new Triplet(-1, -1, -1);
        ans = Math.max(ans, size);
        return new Triplet(min, max, size);
    }

    class Triplet {
        int a;
        int b;
        int c;

        Triplet(int a, int b, int c) {
            this.a = a;
            this.b = b;
            this.c = c;
        }
    }

}

```