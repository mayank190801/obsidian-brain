[[DSA]]

//mark 5 best questions and few questions which needs to be practised no matter what 

//morris traversal 
//inorder and postorder iterative 
//all good questions 
//when to use iterative, recursive and morris traversal (key and their complexities)

## Traversals
In-order traversal  (left + root + right) - recursive
Pre-order traversal (root + left + right) - recursive 
Post-order traversal (left + right + root) - recursive
Level-order traversal (using bfs, queues)  - simple 
[[Iterative Preorder Traversal]]
[[Iterative Inorder Traversal]]
[[Iterative PostOrder Traversal]] (2 stack doable, 1 stack insane)
Iterative postorder inorder (using stack , requires maintain a pair with how many times it occured)

## Binary Tree
Maximum Depth  (Recursive - O(height), Level Order O(N)) 
Check For balanced binary Tree  (if return -1? then always return -1, otherwise return height)
Diameter of binary Tree  (global ans variable, at each level update the ans using height concept )
[[Maximum Path Sum (Good)]]
Check if two trees are identical or not (easy)
[[ZigZag Traversal (Good)]]
Boundary Traversal (I have issues with this question)
[[Vertical Order Traversal (Good)]] 
Top View of Binary Tree (using above traversal)
Bottom View of Binary Tree (same as above, but keep updating your answer set)
[[Right Left Side View (Good)]]
Check for symmetrical Binary Tree (similar to check for binary tree, just reverse left and right)
[[Binary Tree Path (Good)]]
[[Lowest Common Ancestor (Good)]]
Maximum Width of binary tree (similar to top view of binary tree) - iterative / recursion 
[[Children Sum Property (Good)]]
[[Nodes at Distance K (Good)]]  (create a map from child to parent node) - make them a graph!!
Minimum time taken to burn a BT from a node (similar to above)
[[Count Complete Tree nodes (Really Good)]]
Construct a unique binary tree (Condition - Inorder postorder or inorder preorder (atleast))
Construct a unique binary tree from inorder preorder (easy)
Construct a unique binary tree from inorder postorder (easy)
Serialize and Deserialise - (create inorder postorder, or use 1, #, 2, 3, 4, and so on technique)
[[Morris Traversal (GOOOOD)]]
[[Flatten Binary Tree To Linked List (Good)]]

## Binary Search Tree
Search in a BST  (prefer iterative)
Ceil in a BST  (prefer iterative)
Floor in a BST (prefer iterative)
Insert a given node in binary tree  (prefer iterative)
[[Delete a Node in Binary Search Tree (V.Good)]]
Kth smallest Element (using preorder traversal (iterative, recursive, morris))
Kth largest ( 1 traversal for count, then (N - k) the smalelst element finding question)
[[Validate a BST]]
[[LCA in BST (pretty)]]
Construct a BST from preorder traversal 
Inorder Successor/Predessor in BST (simple check if left or right and keep updating the answer)
[[BST Iterator (GOOD)]]
Two Sum in BST (use BST iterator from left and right, and then check if the sum exist or not) 
[[Recover BST (VERY GOOD)]]
[[Largest BST in BT (Good)]]




jj























