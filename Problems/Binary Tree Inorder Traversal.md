### Binary Tree Inorder Traversal.md
#### Writer: Haram Ryu
#### Refer: LeetCode#94 (Easy)
* * *
### Problem
Given the root of a binary tree, return the inorder traversal of its nodes' values.

<b>Example 1</b>
![image](https://user-images.githubusercontent.com/22101375/125283730-a7169d80-e353-11eb-8a0b-e87b36ab4fdb.png)
<pre>
<b>Input</b>: root = [1,null,2,3]
<b>Output</b>: [1,3,2]
</pre>

<b>Example 2</b>
<pre>
<b>Input</b>: root = []
<b>Output</b>: []
</pre>

<b>Example 3</b>
<pre>
<b>Input</b>: root = [1]
<b>Output</b>: [1]
</pre>

<b>Example 4</b>
![image](https://user-images.githubusercontent.com/22101375/125283936-d9c09600-e353-11eb-811d-a15ed32d12a9.png)
<pre>
<b>Input</b>: root = [1,2]
<b>Output</b>: [2,1]
</pre>

<b>Example 5</b>
![image](https://user-images.githubusercontent.com/22101375/125284038-f066ed00-e353-11eb-8816-eb00342768ca.png)
<pre>
<b>Input</b>: root = [1,null,2]
<b>Output</b>: [1,2]
</pre>

#### Constraints
- The number of nodes in the tree is in the range [0, 100].
- -100 <= Node.val <= 100

### Solution
#### Using recursion
```golang
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func inorderTraversal(root *TreeNode) []int {
    res := make([]int,0)
    recursive(root, &res)
    return res
}

func recursive(root *TreeNode, res *[]int) {
    if root == nil {
        return
    }    
    if root.Left != nil {
        recursive(root.Left, res)
    }
    *res = append(*res, root.Val)
    if root.Right != nil {
        recursive(root.Right, res)
    }
}
```
- Extract a number in the index 0. We call it as the comparing number.
- compare it with other numbers in the nums array
- When comparing the numbers, the count increase if the other numbers are bigger than the comparing number.
- When adding the count to the result array, the 'countSmaller' function recursively runs it-self with the nums array except the comparing num.
- The warst timecomplexity is O(n^2) -> O(n) (The comparing for loop) * O(n) (The number of recursive invokations)
