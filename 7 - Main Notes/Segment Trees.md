[[DSA]]


```java
BigIdea
- make a tree, then build it, then query it, and single point update
- index = 0, and hence another indexes are 2*index + 1, 2*index + 2

//
public class pSegmentTree {
        int[] arr;
        int[] tree;
        pSegmentTree(int[] arr){
            //simply store both the arrays in the start
            this.arr = new int[arr.length];
            for(int i = 0; i < arr.length; i++){
                this.arr[i] = arr[i];
            }
            this.tree = new int[arr.length*4 + 1];
        }

        void build(int idx, int low, int high){
            if(low == high){
                tree[idx] = arr[low];
                return;
            }
            int mid = (low + high)/2;
            build(2*idx + 1, low, mid);
            build(2*idx + 2, mid + 1, high);
            tree[idx] = Math.min(tree[2*idx + 1], tree[2*idx + 2]);
        }

        int query(int idx, int low, int high, int l, int r){
            //no overlap
            if(r < low || l > high) return Integer.MAX_VALUE;
            //complete overlap
            if(l <= low && high <= r) return tree[idx];  //achcha jo current low and high, unka scene puch rhe h

            int mid = (low + high)/2;
            int left = query(2 * idx + 1, low, mid, l, r);
            int right = query(2 * idx + 2, mid + 1, high, l, r);
            return Math.min(left, right);
        }

        void update(int idx, int low, int high, int i, int val){
            if(low == high){
                tree[idx] = val;
                return;
            }
            int mid = (low + high)/2;
            if(i <= mid) update(2 * idx + 1, low, mid, i, val);
            else update(2 * idx + 2, mid + 1, high, i, val);
            tree[idx] = Math.min(tree[2*idx + 1], tree[2*idx + 2]);
        }
    }

```