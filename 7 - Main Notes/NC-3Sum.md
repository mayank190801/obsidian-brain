
really cool problem to solve, definitely try agian problem 
Basically you could have skipped hashing using set array but to avoid that 
The solution is beautiful and you have to think about a lot of edges cases


```java 
class Solution {
    //couple of solutions in my mind 
    //one could be to move left and right if duplicates appear 
    //or simply remove the duplicates? 

    //some good edges cases are 
    //duplicates comes up 
    //[0, 0, 0, 0]  -- missed this edge case 
    //and then striver sheet revision asap! (fast and quick!)    

    public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> ans = new ArrayList<>();
        Arrays.sort(nums);    
        System.out.println(Arrays.toString(nums));
        int len = nums.length;
        for(int mid = 0; mid < len; mid++){           
            if(mid > 0 && nums[mid] == nums[mid - 1]) continue;
        
            int left = mid + 1;
            int right = len - 1;
            while(left < right){                       
               
                int sum = nums[left] + nums[mid] + nums[right];                 
                if(sum > 0) right--;
                else if(sum < 0) left++;
                else {                                 
                    ans.add(new ArrayList(Arrays.asList(nums[mid], nums[left], nums[right])));             

                while(left < right && nums[left] == nums[left + 1]) left++;
                while(left < right && nums[right] == nums[right - 1]) right--;
                    left++;
                    right--;
                }                                
            }
        }        
        return ans;
    }
}
```