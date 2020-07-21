#### Invert Binary Tree
#### Writer: Haram Ryu
#### Refer: LeetCode

## 문제 설명
바이너리 트리가 주어지면 거울 대칭으로 뒤집어서 출력하라
***예시***
```
Input: 
     4
   /   \
  2     7
 / \   / \
1   3 6   9
Output: 
     4
   /   \
  7     2
 / \   / \
9   6 3   1
```
## 솔루션
```
func invertTree(root *TreeNode) *TreeNode {
    if root == nil {
        return root
    } 
    
    root.Left, root.Right = root.Right, root.Left
    
    invertTree(root.Left)
    invertTree(root.Right)
    return root
}
```
