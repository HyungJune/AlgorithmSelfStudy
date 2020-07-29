#### Merge Two Binary Trees
#### Writer: Haram Ryu
#### Refer: LeetCode

## 문제 설명
주어진 두개의 바이너리 트리를 루트 노드를 겹쳐서 놓은 다음, 같은 노드에 위치한 값들끼리는 더해서 새로운 바이너리 트리로 만들어서 출력한다.  
***예시***
```
Input: 
	Tree 1                     Tree 2                  
          1                         2                             
         / \                       / \                            
        3   2                     1   3                        
       /                           \   \                      
      5                             4   7                  
Output: 
Merged tree:
	     3
	    / \
	   4   5
	  / \   \ 
	 5   4   7
 ```
 
 ## 솔루션
 ```
 /**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func mergeTrees(t1 *TreeNode, t2 *TreeNode) *TreeNode {
    if t1 != nil && t2 != nil {
        return &TreeNode{
            Val: t1.Val + t2.Val,
            Left: mergeTrees(t1.Left, t2.Left),
            Right: mergeTrees(t1.Right, t2.Right),
        }
    } else if t1 != nil && t2 == nil {
        return &TreeNode{
            Val: t1.Val,
            Left: t1.Left,
            Right: t1.Right,
        }
    } else if t1 == nil && t2 != nil {
        return &TreeNode{
            Val: t2.Val,
            Left: t2.Left,
            Right: t2.Right,
        }
    } else {
        return nil
    }
}
```
- 총 네가지 경우로 구분 가능
    - 1) 입력된 첫번째 트리 노드와 두번째 트리 노드가 모두 nil이 아닌 경우: Val는 두 노드의 Val를 합하고, Left, Right는 재귀적으로 돌린다
    - 2) 첫번째 노드만 nil이 아니고, 두번째 노드는 nil인 경우: 새로운 노드니까 nil이 아닌 노드의 Val를 넣고, Left, Right를 그대로 갖다 넣음
    - 3) 첫번째 노드는 nil이고, 두번째 노드는 nil이 아닌 경우: 위와 동일
    - 4) 둘 다 nil이면 바로 리턴
- 2), 3)의 경우에 그 다음 노드들은 재귀함수로 들어갈 필요는 없는가 → 이미 nil이었던 노드의 아래에는 더 노드가 없으므로, nil이 아닌 노드와 완전히 동일하면 되니까 더 함수처리해야할 필요가 없다
