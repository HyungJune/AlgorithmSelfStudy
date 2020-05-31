#### Data Structure: Binary Search Tree
#### Writer: Haram Ryu
#### Refer: AppliedGo.net

## Properties
1. 트리의 각 노드의 값은 중복되지 않음
2. 각 노드들은 0개, 1개, 2개의 자식 노드를 가질 수 있음
3. 루트 노드라고 지정된 노드는 트리 구조의 꼭대기에 있고, 모든 동작의 엔트리 포인트이다.
4. 루트 노드를 제외한 모든 노드는 부모 노드를 갖는다.
5. 각 노드의 값은 왼쪽 자식 노드의 값보다 크고, 오른쪽 자식 노드의 값보다 작다.
6. 한 노드의 왼쪽 서브트리에 있는 모든 노드의 값은 그 노드의 값보다 작고, 오른쪽 서브트리의 모든 노드의 값은 그 노드의 값보다 크다.

- 자식 노드가 없는 노드는 리프 노드라고 한다.
- 자식 노드가 하나 있는 노드는 하프 리프 노드라고 한다.
- 두 개의 자식 노드가 있는 노드는 이너 노드라고 한다.
- 루프 노드에서 리프 노드까지 가장 긴 경로를 트리의 높이라고 한다.

## Example: Simple Binary Search Tree
### Node Operation
***Insert***  
기본 동작은 단순. 삽입하려는 값을 현재 노드의 값과 비교, Insert Value < Node Value 이면, 현재 노드의 왼쪽 자식 노드와 비교. 이 경우에 왼쪽 자식 노드가 없으면 거기에 그 값을 삽임. Insert > Node Value 이면, 현재 노드의 오른쪽 자식 노드와 다시 비교. 만약 오른쪽 자식 노드가 없으면 거기에 그 값을 삽입. Insert Value == Node Value이면 삽입하지 않음. 이 세 경우로 정리 가능.  
```
type Node struct {
	Value string
	Data  string
	Left  *Node
	Right *Node
}
```
```
func (n *Node) Insert(value, data string) error {

	if n == nil {
		return errors.New("Cannot insert a value into a nil tree")
	}

	switch {

	case value == n.Value:
		return nil

	case value < n.Value:
		if n.Left == nil {
			n.Left = &Node{Value: value, Data: data}
			return nil
		}
		return n.Left.Insert(value, data)

	case value > n.Value:
		if n.Right == nil {
			n.Right = &Node{Value: value, Data: data}
			return nil
		}
		return n.Right.Insert(value, data)
	}
	return nil
}
```
---
***Find***
```
func (n *Node) Find(s string) (string, bool) {

	if n == nil {
		return "", false
	}

	switch {

	case s == n.Value:
		return n.Data, true

	case s < n.Value:
		return n.Left.Find(s)

	default:
		return n.Right.Find(s)
	}
}
```
---
***Delete***
- 지우려는 노드가 리프 노드인 경우: 그 부모 노드에서 그 노드의 포인터를 nil로 바꾸면 됨.
- 지우려는 노드가 하프 리프 노드인 경우: 노드의 값을 자식 노드의 값으로 대체.
- 지우려는 노드가 이너 노드인 경우(동시에 이 노드가 부모 노드에게는 오른쪽 자식 노드라고 가정)
    - 지우려는 노드의 왼쪽 서브트리에서 가장 큰 값을 찾아서 현재 노드를 대체 → 이렇게 안하면, 트리가 꼬이니까.
    - 대체한 노드에 대해서도 똑같이 node delete operation을 적용해야함.
- 이것을 위해서 필요한 두가지 함수가 있음
    - 첫번째는 왼쪽 서브트리에서 가장 큰 값을 찾는 함수.
    - 두번째는 부모 노드에서 지우려는 노드의 포인터를 제거하는 함수. 대체한다고 봐야함.
```
func (n *Node) findMax(parent *Node) (*Node, *Node) {
	if n == nil {
		return nil, parent
	}
	if n.Right == nil {
		return n, parent
	}
	return n.Right.findMax(n)
}

func (n *Node) replaceNode(parent, replacement *Node) error {
	if n == nil {
		return errors.New("replaceNode() not allowed on a nil node")
	}

	if n == parent.Left {
		parent.Left = replacement
		return nil
	}
	parent.Right = replacement
	return nil
}
```
```
func (n *Node) Delete(s string, parent *Node) error {
	if n == nil {
		return errors.New("Value to be deleted does not exist in the tree")
	}

	switch {
	case s < n.Value:
		return n.Left.Delete(s, n)
	case s > n.Value:
		return n.Right.Delete(s, n)
	default:

		if n.Left == nil && n.Right == nil {
			n.replaceNode(parent, nil)
			return nil
		}

		if n.Left == nil {
			n.replaceNode(parent, n.Right)
			return nil
		}
		if n.Right == nil {
			n.replaceNode(parent, n.Left)
			return nil
		}

		replacement, replParent := n.Left.findMax(n)

		n.Value = replacement.Value
		n.Data = replacement.Data

		return replacement.Delete(replacement.Value, replParent)
	}
}
```
### Tree Operation
루트 노드를 표현하기 위해서 Tree라는 structure를 선언함. 트리가 완전히 비어있거나 노드가 하나 밖에 없는 경우를 위해서 이 구조체를 선언한다고 볼 수도 있음. 
```
type Tree struct {
	Root *Node
}

func (t *Tree) Insert(value, data string) error {
	if t.Root == nil {
		t.Root = &Node{Value: value, Data: data}
		return nil
	}
	return t.Root.Insert(value, data)
}

func (t *Tree) Find(s string) (string, bool) {
	if t.Root == nil {
		return "", false
	}
	return t.Root.Find(s)
}

func (t *Tree) Delete(s string) error {

	if t.Root == nil {
		return errors.New("Cannot delete from an empty tree")
	}

	fakeParent := &Node{Right: t.Root}
	err := t.Root.Delete(s, fakeParent)
	if err != nil {
		return err
	}
	if fakeParent.Right == nil {
		t.Root = nil
	}
	return nil
}

func (t *Tree) Traverse(n *Node, f func(*Node)) {
	if n == nil {
		return
	}
	t.Traverse(n.Left, f)
	f(n)
	t.Traverse(n.Right, f)
}
```
