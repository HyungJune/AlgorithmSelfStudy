
### Check If a String Is a Valid Sequence from Root to Leaves Path in a Binary Tree
#### Writer: Hyungjune Shin
#### Refer: LeetCode 
* * *
### Problem

주어진 이진트리에서 valid sequence란 root부터 leaf 노드까지의 값의 순열을 지칭합니다. 주어진 Integer 배열이 있을 때, 해당 배열이 valid sequence를 만족시키는지를 확인하는 프로그램을 작성하는 문제입니다.


<b>Example 1</b>
<pre>
<b>Input</b>: [1,2,3],

    <b>1</b>
   <b>/ \</b>
  <b>2   3</b>

<b>Output</b>: 6
</pre>

<b>Example 2</b>
<pre>
<b>Input</b>: [-10,9,20,null,null,15,7],

   -10
   /  \
  9   <b>20</b>
     <b>/  \</b>
    <b>15   7</b>
    
<b>Output</b>: 42
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
func maxPathSum(root *TreeNode) int {
    max := math.MinInt32
    sum := maxGain(root, &max)
    fmt.Println(sum)
    return max
}

func maxGain(root *TreeNode, max *int) int {
    if root == nil {
        return 0
    }
    
    left := maxFunc(maxGain(root.Left, max), 0)
    right := maxFunc(maxGain(root.Right, max), 0)
    
    sum := root.Val + left + right
    //maxSum := max
    if sum > *max {
        //maxSum = sum
        *max = sum
    }
    return root.Val + maxFunc(left, right)
}

func maxFunc(a int, b int) int {
    if a > b {
        return a
    } else {
        return b
    }
}
```
- 음수값이 존재하므로, max 값을 Integer의 가장 작은 수로 설정합니다.
- 한 노드를 기점으로, 왼쪽 혹은 오른쪽으로 갈 수 있습니다. 이때, max값을 구해야하는 것이므로, 왼쪽 혹은 오른쪽 중 더했을 경우 더 큰 값을 가지는 path를 선택해야합니다. 이와 같은 값의 선택을 위해 maxGain이라는 함수를 구현했습니다.
- 항상 노드의 상위를 거칠 필요가 없고, 그럼에도 전체 max와 subtree에서 발견되는 max값을 비교해야하므로, maxGain 함수는 tree의 전체 max 값을 계속해서 들고 있으며, 만약 subtree에서 max 값보다 큰 path 값이 결정될 경우에 update 합니다.
- 이때, maxGain에서 갈 수 있는 패스는 1) 노드를 기점으로 왼쪽, 오른쪽 path 중 하나를 고르고 상위 노드를 거쳐 간다 2) 상위 노드를 거치지 않는다라는 선택지가 존재하며, 재귀함수 특성 상 상위노드를 거치지 않을 경우 값의 계산이 끝나므로 max 값과 비교를하여 update를 시도하며, 1)일 경우에는 상위노드에서 계산이 필요하므로 해당 값을 return 시켜 줍니다.
- 결국, maxGain함수에 root 노드일 경우에 나오는 max 값이 해답이 됩니다.
