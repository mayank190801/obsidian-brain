[[DSA]]
[[Tree DSA]]


//good question to practise and revise some core concepts I believe 

- use triplet to store node, level and col 
- then add them in a treeMap 
- in the end go through the keyset of treemap  and then sort the collections and create your answer


```java
class Solution {

    public List<List<Integer>> verticalTraversal(TreeNode root) {
        if (root == null)
            return new ArrayList<>(); // no work is required in this case
        Map<Integer, List<Pair>> map = new TreeMap<>();

        ArrayDeque<Pair> que = new ArrayDeque<>();
        que.add(new Pair(root, 0));

        int level = 0;
        while (!que.isEmpty()) {
            int size = que.size();
            while (size-- > 0) {
                Pair curr = que.poll();
                TreeNode currTree = curr.node;
                int col = curr.col;
                map.putIfAbsent(col, new ArrayList<>());
                map.get(col).add(new Pair(currTree, level));
                if (currTree.left != null)
                    que.add(new Pair(currTree.left, curr.col - 1));
                if (currTree.right != null)
                    que.add(new Pair(currTree.right, curr.col + 1));
            }
            level++;
        }

        List<List<Integer>> ans = new ArrayList<>();
        for (int key : map.keySet()) {
            // System.out.println(key);
            List<Integer> list = new ArrayList<>();
            List<Pair> keyList = map.get(key);
            Collections.sort(keyList,
                    (a, b) -> Integer.compare(a.col, b.col) == 0 ? Integer.compare(a.node.val, b.node.val)
                            : Integer.compare(a.col, b.col));
            for (Pair p : keyList) {
                list.add(p.node.val);
            }
            ans.add(list);
            // System.out.println(list);
        }

        return ans;
    }

    public class Pair {
        TreeNode node;
        int col;

        Pair(TreeNode node, int col) {
            this.node = node;
            this.col = col;
        }
    }
}

```