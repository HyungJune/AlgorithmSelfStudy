### Count of Smaller Numbers After Self
#### Writer: Hyungjune Shin
#### Refer: LeetCode (Hard)
* * *
### Problem
You are given an integer array nums and you have to return a new counts array. The counts array has the property where counts[i] is the number of smaller elements to the right of nums[i].

<b>Example 1</b>
<pre>
<b>Input</b>: nums = [5,2,6,1]
<b>Output</b>: [2,1,1,0]
<b>Explanation</b> 
To the right of 5 there are 2 smaller elements (2 and 1).
To the right of 2 there is only 1 smaller element (1).
To the right of 6 there is 1 smaller element (1).
To the right of 1 there is 0 smaller element.
</pre>

<b>Example 2</b>
<pre>
<b>Input</b>: nums = [-1]
<b>Output</b>: [0]
</pre>

<b>Example 3</b>
<pre>
<b>Input</b>: nums = [-1,-1]
<b>Output</b>: [0,0]
</pre>

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
