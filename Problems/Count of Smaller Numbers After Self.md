### Count of Smaller Numbers After Self
#### Writer: Hyungjune Shin
#### Refer: LeetCode
* * *
### Problem
You are given an integer array nums and you have to return a new counts array. The counts array has the property where counts[i] is the number of smaller elements to the right of nums[i].



#### Constraints
- 0 <= digits.length <= 4
- digits[i] is a digit in the range ['2', '9'].

### Solution
#### First Naive Solution
```java
class Solution {
    public List<Integer> countSmaller(int[] nums) {
      if(nums.length == 1) {
        List<Integer> result = new ArrayList<>();
        result.add(0);
        return result;
      }

      int compare = nums[0];
      int count = 0;
      for(int i=1; i<nums.length; i++){
        if(compare > nums[i]) count++;
      }
      List<Integer> result = new ArrayList<>();
      result.add(count);
      result.addAll(
        countSmaller(Arrays.copyOfRange(nums, 1, nums.length))
      );
      return result;
    }
}
```
