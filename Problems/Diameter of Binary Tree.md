### Diameter of Binary Tree
#### Writer: Haram Ryu
#### Refer: LeetCode#543 (Easy)
* * *
### Problem
Given the root of a binary tree, return the length of the diameter of the tree.

The diameter of a binary tree is the length of the longest path between any two nodes in a tree. This path may or may not pass through the root.

The length of a path between two nodes is represented by the number of edges between them.

<b>Example 1</b>
![image](https://user-images.githubusercontent.com/22101375/136013698-eb410dc2-1c9f-4412-ba32-ef4f4420739e.png)

<pre>
<b>Input</b>: root = [1,2,3,4,5]
<b>Output</b>: 3
<b>Explanation</b>: 3 is the length of the path [4,2,1,3] or [5,2,1,3].
</pre>


#### Constraints
- The number of nodes in the tree is in the range [1, 10^4].
- -100 <= Node.val <= 100

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
func diameterOfBinaryTree(root *TreeNode) int {
        
    if root == nil {
        return 0
    }
    
    dia := 0
    
    longestDepth(root, &dia)
    
    return dia
}

func longestDepth(root *TreeNode, resDia *int) int {
    leftDepth := 0
    rightDepth := 0
    
    if root == nil {
        return 0
    }
    
    if root.Left != nil {
        leftDepth = longestDepth(root.Left, resDia) + 1
    }
    
    if root.Right != nil {
        rightDepth = longestDepth(root.Right, resDia) + 1
    }
    
    *resDia = max(*resDia, leftDepth+rightDepth)

    return max(leftDepth, rightDepth)
}

func max(x int, y int) int {
    if x > y {
        return x
    } else {
        return y
    }
}
```
- Postorder traversal(후위순회): 왼쪽→오른쪽→루트
- recusive function으로 후위순회를 하면서 root 노드에서 왼쪽으로 가장 긴 깊이와 오른쪽으로 가장 긴 깊이를 찾아서 더한 값을, global maximum과 비교해가며 
