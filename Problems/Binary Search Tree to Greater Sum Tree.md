#### 1038. Binary Search Tree to Greater Sum Tree
#### Writter: Donggyu Cho
#### Refer: LeetCode

## 문제설명
Given the root of a binary search tree with distinct values, modify it so that every node has a new value equal to the sum of the values of the original tree that are greater than or equal to node.val.


<b>Example 1</b>
<pre>
<img src="./images/leetcode_binary_search_tree_to_greater_sum_tree_1.PNG" alt="drawing" width="300" />
<b>Input</b>: [4,1,6,0,2,5,7,null,null,null,3,null,null,null,8]
<b>Output</b>: [30,36,21,36,35,26,15,null,null,null,33,null,null,null,8]
</pre>

<b>Constraints</b>
<pre>
<b> node의 개수는 1~100 사이이다. </b>
<b> 각 노드는 0~100 사이의 값을 갖는다. </b>
<b> 주어진트리는 이진 탐색 트리이다. </b>
</pre>

* * *
### Solution
아직 미완성...
```go
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
```
```go
package main

type TreeNode struct {
	Val   int
	Left  *TreeNode
	Right *TreeNode
}

type stack struct {
	arr   []*TreeNode
	count int
}

func (s *stack) Push(node *TreeNode) {
	s.arr = append(s.arr[:s.count], node)
	s.count++
}

func (s *stack) Pop() *TreeNode {
	if s.count == 0 {
		return nil
	}
	s.count--
	return s.arr[s.count]
}

func (s *stack) isEmpty() bool {
	if s.count == 0 {
		return true
	}
	return false
}

func main() {
}
func bstToGst(root *TreeNode) *TreeNode {

	return root
}

func search(root *TreeNode, s *stack) *TreeNode {
	var node *TreeNode
	if root == nil {
		return root
	}

	node = root.Right

	for {
		// if node == nil {
		// 	return s.Pop()
		// }

		if node.Right != nil {
			s.Push(node)
			search(node.Right, s)
		} else {
			return s.Pop()
		}

		node.Val += node.Right.Val

		if node.Left != nil {

		}
	}

	return root
}

func search2(root *TreeNode, s *stack) *TreeNode {
	if root.Right != nil {
		s.Push(root)
		search2(root.Right, s)
	}
	triangle(root)
	if root.Left != nil {
		s.Push(root)
		search2(root.Left, s)
	}

	var tmp *TreeNode
	tmp = s.Pop()
	if tmp.Left == root {
		root.Val += tmp.Val
	}
	return s.Pop()
}

func triangle(node *TreeNode) {
	if node.Right != nil {
		node.Val += node.Right.Val
	}
	// if node.Left != nil {
	// 	node.Left.Val = node.Val + node.Left.Val
	// }
}

/*
func genBSTArr(root *TreeNode) []int {
	var bstArr []int
	var depthQueue *queue
	bstArr = make([]int, 0)
	depthQueue = &queue{}
	depthQueue.initialize(0)

	var tmp *TreeNode
	index := 0
	depth := 1

	depthQueue.Push(root)

	for {
		for i := 0; i < 2^depth;
		tmp = depthQueue.Pop().(*TreeNode)
		if tmp == nil {

		} else {
			bstArr[index] = tmp.Val
			index++

			if tmp.Left != nil {
				depthQueue.Push(tmp.Left)
			} else {
				depthQueue.Push(nil)
			}
			if tmp.Right != nil {
				depthQueue.Push(tmp.Right)
			} else {
				depthQueue.Push(nil)
			}
		}
		depth++
	}

	return bstArr
}
*/

type queue struct {
	front int
	rear  int
	size  int
	arr   []interface{}
}

func (q *queue) doublingSlice() {
	var doubledSlice []interface{}
	doubledSlice = make([]interface{}, len(q.arr), cap(q.arr)*2)
	copy(doubledSlice, q.arr)
	q.arr = doubledSlice
	q.size = cap(q.arr)
}

func (q *queue) initialize(args interface{}) {
	const DEFAULT_SIZE = 10

	switch args.(type) {
	case int:
		if args.(int) == 0 {
			q.size = DEFAULT_SIZE
		} else {
			q.size = args.(int)
		}
	default:
		q.size = DEFAULT_SIZE
	}
	q.arr = make([]interface{}, q.size, q.size)
	q.front = 0
	q.rear = 1
}

func (q *queue) Push(elem interface{}) {
	if len(q.arr) == cap(q.arr) {
		q.doublingSlice()
	}
	q.arr[q.rear-1] = elem
	q.rear = (q.rear + 1) % q.size
}

func (q *queue) Pop() (elem interface{}) {
	elem = q.arr[q.front]
	q.front = (q.front + 1) % q.size
	return elem
}

func (q *queue) isEmpty() bool {
	if q.front == q.rear {
		return true
	}
	return false
}
```

### 접근법

Search()를 통해 우선 트리에서 가장 큰 값을 가지는 노드로 이동.
그 노드부터 Subtree를 구성. 현재 정의한 Subtree란 노드, 노드.left와 노드.right로 이루어져 있다. 

Search(root *TreeNode) : Input으로 받는 Root로부터 탐색을 시작하는 동작 수행
modify(root *TreeNode) : 하나의 노드 그리고 left와 right를 가진 3개의 노드 조합을 subtree로 정의하고 해당 subtree 에서 example과 같은 값의 변화를 주는 동작 수행


