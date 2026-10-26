
[[DSA]]
[[Tree DSA]]
[[Java Collections Framework]]


- Reallly good question, do implement it once 


//let's write this learning down brother, pretty cool that we figured this out 


```java
Object a;  //xyz
Object b;  //zyx

//in total we have 2 pointers - a, b 

Swap(Object x, Object y){
	//in total we have 4 pointers - a, b , x, y
	// a = xyz, b = zyx, x = xyz, y = zyx

	Object temp = x; 
	x = y;
	y = temp;


	//in total we have 4 pointers again 
	//a = xyz, b = zyx, x = zyx, y = xyz
}


//hence the swap for the object referece for a and b is not possible 
//you can change the value present inside the object but not the referenece itself 
```


- YOU NEED TO MAINTAIN A PREVIOUS POINTER 
//Why? because curr = curr.right (are not inorder successor of each other!!! DUMB FUCK)


```java
class Solution {
    //HIGH DIFFICULTY 
    TreeNode a = null, b = null, prev = null;
    public void recoverTree(TreeNode root) {    
        TreeNode curr = root;
        while(curr != null){
            if(curr.left != null){
                TreeNode temp = curr.left;
                while(temp.right != null && temp.right != curr){
                    temp = temp.right;
                }
                if(temp.right == curr){
                    temp.right = null;
                    check(prev, curr);
                    prev = curr;
                    curr = curr.right;
                }else{
                    temp.right = curr;
                    curr = curr.left;
                }
            }else{
                check(prev, curr);
                prev = curr;
                curr = curr.right;
            }
        }        
        swap(a,b);
    }

    public void check(TreeNode x, TreeNode y){
        if(x == null || y == null) return;
        System.out.println(x.val + " " + y.val);
        if(x.val > y.val){
            if(a == null) a = x;
            b = y;            
        }
    }

    public void swap(TreeNode x, TreeNode y){
        int temp = x.val;
        x.val = y.val;
        y.val = temp;
    }
}
```

