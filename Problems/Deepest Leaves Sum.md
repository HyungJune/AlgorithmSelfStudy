
### Deepest Leaves Sum
#### Writer: Hyungjune Shin
#### Refer: LeetCode#1302
* * *
### Problem
Given a binary tree, return the sum of values of its deepest leaves.

<b>Example 1</b>

![Example1](https://github.com/HyungJune/AlgorithmSelfStudy/blob/master/Problems/images/leetcode_deepest_leaves_sum_ex1.png)

<pre>
<b>Input:</b> root = [1,2,3,4,5,null,6,7,null,null,null,null,8]
<b>Output:</b> 15
</pre>
* * *
### Solution
```go
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func deepestLeavesSum(root *TreeNode) int {
    result, _ :=deepestLeaves(root, 0)
    return result
}

func deepestLeaves(node *TreeNode, depth int) (int, int) {
    if node.Left == nil && node.Right == nil {
        return node.Val, depth+1
    } else if node.Left == nil && node.Right != nil {
        return deepestLeaves(node.Right, depth+1)
    } else if node.Left != nil && node.Right == nil {
        return deepestLeaves(node.Left, depth+1)
    }
    
    leftVal, leftDepth := deepestLeaves(node.Left, depth+1)
    rightVal, rightDepth := deepestLeaves(node.Right, depth+1)
    
    if leftDepth > rightDepth {
        return leftVal, leftDepth
    } else if rightDepth > leftDepth{
        return rightVal, rightDepth
    } else {
        return rightVal + leftVal, leftDepth
    }
    
}
```
- 가장 depth가 깊은 노드들의 (Leaves의) 합을 구하는 문제입니다.
- 단순히 leaves에 대한 합이 아니므로 depth 값을 알아야합니다.
- deepestLeaves는 현재 노드에서 가장 depth가 큰 노드의 값을 선택하고, 만약 왼쪽, 오른쪽 방향으로 탐색했을 때 깊이가 같을 경우에는 그 합을 반환합니다.
- 재귀적 방식으로 depth를 매개변수로 주고, 다시 반환받는 형식으로 구성이 되었습니다.
