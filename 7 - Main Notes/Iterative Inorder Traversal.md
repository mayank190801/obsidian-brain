
[[DSA]]
[[Tree DSA]]

- Best code out there 
- You don't need to memorize the code
- Just remember one while (true) loop can make it possible
- Pick and put all right left element and so on 

```java
class Solution {
	public List<Integer> inorderTraversal(TreeNode root){
		Deque<Integer> st = new ArrayDeque<>();
		List<Integer> order = new ArrayList<>();
		TreeNode curr = root; 
		while(true){
			if(curr != null){
				st.push(curr);
				curr = curr.left;
			}else{
				if(st.isEmpty()) break;
				curr = st.pop();
				order.add(curr.val);
				curr = curr.right;
			}
		}
		return order;
	}
}
```