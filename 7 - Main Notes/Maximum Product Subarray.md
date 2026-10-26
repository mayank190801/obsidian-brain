
Tags : [[Dynamic Programming DSA]]

https://leetcode.com/problems/maximum-product-subarray/description/


Two Solutions 
- Intuitive Approach 
- Kadane Algorithm
- Personal Approach 

Intuitive Approach 
- Solve for both left and right simultaneously 
- If last time zero, then it should be 1 
- Use double because it can handle way big values compared to int/long 
```
    public int maxProduct(int[] nums) {
        int ans = Integer.MIN_VALUE;
        double left = 1;
        double right = 1;
        
        for(int i = 0; i < nums.length; i++){
            if(left == 0) left = 1;
            if(right == 0) right = 1;

            left = left * nums[i];
            right = right * nums[nums.length - 1 - i];
            
            ans = Math.max(ans, Math.max((int) left, (int) right));
        }
        return ans;
    }
```

My Personal Implementation (Annoyingly long)
```
public int maxProduct(int[] nums) {
        if(nums.length == 1) return nums[0];
        int start = 0;
        int[] ans = new int[1];
        for(int i = 0; i < nums.length; i++){
            if(nums[i] == 0){
               subarraySolver(nums, start, i - 1, ans);
               start = i + 1;
            }
        }
        subarraySolver(nums, start, nums.length-1, ans);
        return ans[0];
    }

    public void subarraySolver(int[] nums, int i, int j, int[] ans){
        if(i > j) return;
        List<Integer> list = new ArrayList<>();
        for(int k = i; k <= j; k++){
            if(nums[k] < 0) list.add(k);
        }
        if(list.size() % 2 == 0){
            ans[0] = Math.max(ans[0], returnMaxInRange(nums, i, j));
        }else{
            ans[0] = Math.max(Math.max(returnMaxInRange(nums, i, list.get(list.size() - 1) - 1), returnMaxInRange(nums, list.get(0) + 1, j)), ans[0]);
        }
    }

    public int returnMaxInRange(int[] nums, int i, int j){
        if(i > j) return 0;
        int answer = 1;
        for(int k = i; k <= j; k++){
            answer = answer * nums[k];
        }
        return answer;
    }
```

