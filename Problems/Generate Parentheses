### Generate Parentheses
#### Writer: Donggyu Cho
#### Refer: LeetCode#22 (Medium)
* * *
### Problem
Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

<b>Example 1</b>
<pre>
<b>Input</b>: n = 3
<b>Output</b>: ["((()))","(()())","(())()","()(())","()()()"]
</pre>

<b>Example 2</b>
<pre>
<b>Input</b>: n = 1
<b>Output</b>: ["()"]
</pre>


#### Constraints
- 1 <= n <= 8

### Solution
```python
class Node:
    def __init__(self, data = "", sum = 0, count = 0) -> None:
        if data=="":
            print("initialize")
        self.data = data
        self.sum = sum
        self.count = count
        self.left = None
        self.right = None
    def insert(self, data, sum, count, left, right) :
        if left :
            self.left = Node(data, sum, count)
        if right :
            self.right = Node(data, sum, count)

class Solution:
    def __init__(self) -> None:
        self.root = Node()

    def generateParenthesis(self, n: int) -> List[str]:
        l = []
        self.dfs(self.root, 0, 0, 2*n, l)
        return l

    def dfs(self, node: Node, left:int, current:int, depth:int, l: List[str]):
        if current > depth :
            return 
        if left < depth/2 :
            if node.left == None:
                node.left = Node(node.data+"(", node.sum+1, node.count+1)
            self.dfs(node.left, left+1, current+1, depth, l)
        if node.sum > 0 :
            if node.right == None:
                node.right = Node(node.data+")", node.sum-1, node.count+1)
            self.dfs(node.right, left, current+1, depth, l)
        if node.count == depth:
            l.append(node.data)
```

- Binary Tree를 그리며 "("를 추가하면 left, ")"를 추가하면 ")"가 추가되는 문자열을 만든다
- 만드는 과정 속에서 ")"의 개수가 "("의 개수를 넘지 않도록 하며 "("의 개수는 n 값을 넘지 않도록 하며 트리를 만든다
- 이렇게 만들어둔 Tree는 추후에 재사용 될 수 있지 않을까 생각한다
- depth가 2*n이 되는 leaf들이 n에 대한 답이 된다
