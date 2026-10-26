
```java

class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int left = 0;
        int right = numbers.length - 1;
        while(left < right){
            int sum = numbers[left] + numbers[right];
            if(sum > target) right--;
            else if(sum < target) left++;
            else return new int[]{left + 1, right + 1};
        }
        return new int[2];
    }
}

Learnings 
No solution is ever skipped because:
- If a solution involved R, it must be with a number smaller than current R
- If a solution involved L, it must be with a number larger than current L
```