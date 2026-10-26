
[[DSA]]
[[Stack and Queue DSA]]

Best Method 
```java
class Solution {    
    public int[] maxSlidingWindow(int[] nums, int k) {
        int n = nums.length;
        Deque<Pair> deque = new ArrayDeque<>();
        int[] ans = new int[n - k + 1];
        int aidx = 0;
        for(int i = 0; i < n; i++){
            //remove from the deque if anyone needs to be removed            
            while(!deque.isEmpty() && deque.getFirst().idx <= (i - k)){
                deque.removeFirst();
            }

            //add in the queue in sexy manner
            while(!deque.isEmpty() && deque.getLast().val < nums[i]){
                deque.removeLast();
            }
            deque.addLast(new Pair(nums[i], i));

            //when to add in answer
            if(i - k >= -1){
                ans[aidx++] = deque.getFirst().val;
            }
        }
        return ans;
    }

    class Pair {
        int val;
        int idx;
        Pair(int val, int idx){
            this.val = val;
            this.idx = idx;
        }
    }
}
```


Method way - Priority Queue!! (pretty cool heap solution)
```java
class Solution {    
    public int[] maxSlidingWindow(int[] nums, int k) {
        int n = nums.length;
        PriorityQueue<Pair> pq = new PriorityQueue<>((a, b) -> Integer.compare(b.val, a.val));
        for(int i = 0; i < k - 1; i++){
            pq.add(new Pair(nums[i], i));
        }
        int[] ans = new int[n - k + 1];
        int aidx = 0;
        for(int i = k - 1; i < n; i++){            
            pq.add(new Pair(nums[i], i));
            while(!pq.isEmpty() && pq.peek().idx <= i - k){
                pq.poll();
            }
            Pair curr = pq.peek();
            ans[aidx++] = curr.val;
        }
        return ans;
    }

    class Pair {
        int val;
        int idx;
        Pair(int val, int idx){
            this.val = val;
            this.idx = idx;
        }
    }
}
```



