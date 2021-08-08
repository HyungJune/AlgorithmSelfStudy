### 4Sum
#### Writer: Hyungjune Shin
#### Refer: LeetCode (#18) - Medium
* * *
### Problem
Given an array nums of n integers, return an array of all the unique quadruplets [nums[a], nums[b], nums[c], nums[d]] such that:

- 0 <= a, b, c, d < n
- a, b, c, and d are distinct.
- nums[a] + nums[b] + nums[c] + nums[d] == target

You may return the answer in any order.

<b>Example 1:</b>
<pre>
<b>Input</b>: nums = [1,0,-1,0,-2,2], target = 0
<b>Output</b>: [[-2,-1,1,2],[-2,0,0,2],[-1,0,0,1]]
</pre>

<b>Example 2:</b>
<pre>
<b>Input</b>: nums = [2,2,2,2,2], target = 8
<b>Output</b>: [[2,2,2,2]]
</pre>

#### Constraints
- 1 <= nums.length <= 200
- -109 <= nums[i] <= 109
- -109 <= target <= 109
* * *
### Solution
#### Two Point 방식
```java
class Solution {
    public List<List<Integer>> fourSum(int[] nums, int target) {
		Arrays.sort(nums);
		return kSum(nums, target, 0, 4);
	}

	public List<List<Integer>> kSum(int[] nums, int target, int start, int k) {
		List<List<Integer>> result = new ArrayList<>();
		if(start == nums.length || nums[start] * k > target || target > nums[nums.length-1] * k)
			return result;
		if(k==2)
			return twoSum(nums, target, start);
		else
			for(int i = start; i<nums.length;i++)
				if( i==start || nums[i] != nums[i-1])
					for(List<Integer> subset : kSum(nums, target-nums[i],i+1, k-1)){
						result.add(new ArrayList<>(Arrays.asList(nums[i])));
						result.get(result.size()-1).addAll(subset);
					}
        return result;
	}

	public List<List<Integer>> twoSum(int[] nums, int target, int start) {
		List<List<Integer>> result = new ArrayList<>();
		int lo = start;
		int hi = nums.length-1;
		while(lo < hi) {
			int sum = nums[lo] + nums[hi];
			if(sum < target || lo > start && nums[lo] == nums[lo-1]) lo++;
			else if(sum > target || hi < nums.length-1 && nums[hi] == nums[hi+1]) hi--;
			else {
				result.add(Arrays.asList(nums[lo++], nums[hi--]));
			}
		}
		return result;
	}
}
```
- It is first to sort the input array.
- We should implement kSum function (k = 4 in this problem)
- The minimum value of k is 2. In that case, it is twoSum.
- kSum function picks a value from left (smallest) to right (biggest). Afterthat, gets the subset from (k-1)Sum with the substracted target value by the picked value. The answsers are the lists containing the picked values and the subsets.


