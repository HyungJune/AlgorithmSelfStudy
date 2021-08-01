### Convert Sorted Array to Binary Search Tree
#### Writer: Haram Ryu
#### Refer: LeetCode#108 (Easy)
* * *
### Problem
Given an integer array nums where the elements are sorted in ascending order, convert it to a height-balanced binary search tree.

A height-balanced binary tree is a binary tree in which the depth of the two subtrees of every node never differs by more than one.

<b>Example 1</b>
![image](https://user-images.githubusercontent.com/22101375/127760233-f1c1f4d4-fde8-4f92-bf04-167be961ed01.png)
<pre>
<b>Input</b>: nums = [-10,-3,0,5,9]
<b>Output</b>: [0,-3,9,-10,null,5]
<b>Explanation</b>: [0,-10,5,null,-3,null,9] is also accepted:
</pre>
![image](https://user-images.githubusercontent.com/22101375/127760241-c184a6ae-7869-4e85-8713-44464cb01297.png)

#### Constraints
- 1 <= nums.length <= 10^4
- -10^4 <= nums[i] <= 10^4
- nums is sorted in a strictly increasing order.

### Solution
```golang
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func sortedArrayToBST(nums []int) *TreeNode {
	if len(nums) == 0 {
		return nil
	}
  
	root := TreeNode{}
	idx := len(nums)/2 + 1
	root.Val = nums[idx-1]
	fmt.Printf("idx = %d\n", idx)
	fmt.Printf("root.Val = %d\n", root.Val)
	fmt.Printf("nums[:idx-1] = %d\n", nums[:idx-1])
	fmt.Printf("nums[idx:] = %d\n", nums[idx:])
	root.Left = sortedArrayToBST(nums[:idx-1])
	root.Right = sortedArrayToBST(nums[idx:])

	return &root
}
```
- 입력이 sorted array로 들어오니까 array의 중간 인덱스를 기준으로 중앙값은 root.Val로, 왼쪽 배열은 root.Left 트리로, 오른쪽 배열은 root.Right 트리로 구성을 반복하면됨
- 다음 sortedArrayToBST로 넘기는 nums[:idx-1]가 nums[0:1]이 되면 len(nums)는 0이 되고 root에 들어갈 값이 없기 때문에(nil) 종료 조건 len(nums) == 0으로 처리
