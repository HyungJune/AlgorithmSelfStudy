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

### 접근법

Search()를 통해 우선 트리에서 가장 큰 값을 가지는 노드로 이동.
그 노드부터 Subtree를 구성. 현재 정의한 Subtree란 노드, 노드.left와 노드.right로 이루어져 있다. 

Search(root *TreeNode) : Input으로 받는 Root로부터 탐색을 시작하는 동작 수행
modify(root *TreeNode) : 하나의 노드 그리고 left와 right를 가진 3개의 노드 조합을 subtree로 정의하고 해당 subtree 에서 example과 같은 값의 변화를 주는 동작 수행


