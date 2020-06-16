#### Maximum Depth of Binary Tree
#### Writer: Haram Ryu
#### Refer: LeetCode

## 문제 설명
바이너리 트리의 최대 깊이(depth)를 구하는 문제. 깊이란 루트 노드로부터 가장 먼 잎새 노드까지의 길이를 의미.

***예시***
```
    3
   / \
  9  20
    /  \
   15   7
```
- 위의 경우는 depth 3

## 솔루션
- 다음 노드로 넘어갔을 때의 액션을 함수로 정의하고, 재귀함수를 돌린다. 다음 노드로 넘어갔을 때 케이스는 다음 세가지
    - 1) node.Left != nil인 경우
    - 2) node.Right != nil인 경우
    - 3) 그 외(node.Left == nil && node.Right == nil)인 경우
- 이 경우를 의미하는 함수가 nextNode
```
func nextNode(node *TreeNode, depth int) int {
    if node.Left != nil {
        return nextNode(node.Left, depth + 1)
    } else if node.Right != nil {
        return nextNode(node.Right, depth + 1)
    } else {
        return depth + 1
    }
}
```
- maxDepth 함수는 LeetCode에서 제공된 함수로, nextNode를 호출하는 함수인데, root 노드에 대한 경우를 처리한다
    - root 노드가 없는 경우 0을 바로 리턴
    - root 노드만 있는 경우 1을 바로 리턴
    - root.Left == nil인 경우 → Right에 대해 nextNode 실행
    - root.Right == nil인 경우 → Left에 대해 nextNode 실행
    - 그 외의 경우 Left, Right 중에 nextNode 실행한 것에 대해 최대값 구하기
```
func maxDepth(root *TreeNode) int {
	var prevDepth int = 1
	if root == nil {
		return 0
	} else if root.Left == nil && root.Right == nil {
		return 1
	} else if root.Left == nil {
		return nextNode(root.Right, prevDepth)
	} else if root.Right == nil {
		return nextNode(root.Left, prevDepth)
	}
	return max(nextNode(root.Left, prevDepth), nextNode(root.Right, prevDepth))
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



func maxDepth(root *TreeNode) int {
	var prevDepth int = 1
	if root == nil {
		return 0
	} else if root.Left == nil && root.Right == nil {
		return 1
	} else if root.Left == nil {
		return nextNode(root.Right, prevDepth)
	} else if root.Right == nil {
		return nextNode(root.Left, prevDepth)
	}
	return max(nextNode(root.Left, prevDepth), nextNode(root.Right, prevDepth))
}


func nextNode(node *TreeNode, depth int) int {
    if node.Left != nil {
        return nextNode(node.Left, depth + 1)
    } else if node.Right != nil {
        return nextNode(node.Right, depth + 1)
    } else {
        return depth + 1
    }
}

func max(a, b int) int {
    if a > b {
        return a
    } else {
        return b
    }
}
```
## 제출 결과
- 예외처리를 하는 도중, [3, 4, 5, -7, -6, nil, nil, -7, nil, -5, nil, nil, nil, nil, -4] 인 경우가 나와서 진행이 불가능했..
- golang에 대한 케이스 처리가 좀 잘못 된듯
