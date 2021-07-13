### Binary Tree Inorder Traversal
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
#### Trivial recursive solution
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
- Preorder traversal(전위순회): 루트→왼쪽→오른쪽
- Postorder traversal(후위순회): 왼쪽→오른쪽→루트
- Inorder traversal(중위순회): 왼쪽→루트→오른쪽
- 시간복잡도 O(n), 공간복잡도: O(n)
#### Iterative solution
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
    tmp := make([]*TreeNode,0)
    
    for root != nil || len(tmp) != 0 {
        for root != nil {
            tmp = append(tmp, root)
            root = root.Left
        }
        root = tmp[len(tmp)-1]
        res = append(res, tmp[len(tmp)-1].Val)
        tmp = tmp[0:len(tmp)-1]
        root = root.Right
    }
    return res
}
```
- golang에는 stack이 없으니 slice를 stack처럼 활용
- 먼저 가장 왼쪽 노드를 찾으며 그 과정에 있는 노드를 tmp 슬라이스에 뒤쪽으로 append
- tmp 슬라이스 가장 마지막 값을 꺼내서 다시 root에 저장
- result 슬라이스에 값을 추가
- root를 Right노드로 넣어 거기서부터 다시 가장 왼쪽 노드를 찾는 중위순회를 반복
- 시간복잡도 O(n), 공간복잡도 
