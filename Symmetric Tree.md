#### Symmetric Tree
#### Writer: Haram Ryu
#### Refer: LeetCode

## 문제 설명
주어진 바이너리트리가 대칭인지 아닌지 판별한다.  
***예시***  
다음 바이너리 트리는 대칭
```
    1
   / \
  2   2
 / \ / \
3  4 4  3
```
***예시***  
다음 바이너리 트리는 대칭이 아님
```
    1
   / \
  2   2
   \   \
   3    3
```

## 솔루션
- 이것도 재귀함수 이용
- compareTwoNode
    - 두 노드를 비교하는 함수, 두 노드가 둘 다 nil이거나, 둘 중 하나가 nil일 때까지 비교한다.(어디서 끊을지가 중요하지 않나..)
    - 만약 두 노드의 값이 같다면, 첫번째 노드의 왼쪽 서브트리와 두번째 노드의 오른쪽 서브트리를 비교하고, 첫번째 노드의 오른쪽 서브트리와 두번째 노드의 왼쪽 서브트리를 비교
 ```
func compareTwoNode(n1, n2 *TreeNode) bool {
    if n1 == nil && n2 == nil {
        return true
    } 
    if n1 == nil || n2 == nil {
        return false
    }
    return n1.Val == n2.Val && compareTwoNode(n1.Left, n2.Right) && compareTwoNode(n1.Right, n2.Left)
}
```
```
 /**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func isSymmetric(root *TreeNode) bool {
    return compareTwoNode(root, root)
}
```
