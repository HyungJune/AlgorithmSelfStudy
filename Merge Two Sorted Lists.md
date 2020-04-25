#### Merge Two Sorted Lists
#### Writer: Haram Ryu
#### Refer: LeetCode

## 문제 설명
두 개의 linked list가 입력된다. 각각의 linked list는 숫자 오름차순으로 정렬이 된 상태. 입력된 두 linked list를 병합된 하나의 linked list로 나타내되 역시 숫자 오름차순으로 정렬하여 병합된 하나의 linked list로 나타내어야한다.
***예시***
```
Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4
```
## 솔루션
```
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
type List struct {
	head *ListNode
	tail *ListNode
}

func (l *List) first() *ListNode {
	return l.head
}

func (l *List) push(value int) {
	node := &ListNode{Val: value}
	if l.head == nil {
		l.head = node
	} else {
		l.tail.Next = node
	}
	l.tail = node
}

func mergeTwoLists(l1 *ListNode, l2 *ListNode) *ListNode {
    	output := &List{}
	for {
		if l1 != nil && l2 != nil && l1.Val <= l2.Val {
			output.push(l1.Val)
			l1 = l1.Next
		} else if l1 != nil && l2 != nil && l1.Val > l2.Val {
			output.push(l2.Val)
			l2 = l2.Next
		} else if l1 != nil && l2 == nil {
			output.push(l1.Val)
			l1 = l1.Next
		} else if l1 == nil && l2 != nil {
			output.push(l2.Val)
			l2 = l2.Next
		}
		if l1 == nil && l2 == nil {
			break
		}
	}
	n := output.first()
    return n
}
```
- Linked list의 조작에 필요한 push(), first() 함수를 구현, head와 tail값을 갖는 List 구조체도 구현(인터넷 코드 참조)
    - push() 함수는 linked list 뒤에 추가하는 함수
    - first() 함수는 List의 첫번째 ListNode 구조체의 주소를 반환하는 함수
- if 조건문은 순서대로 다음과 같은 의미를 갖는다
    - l1과 l2가 모두 nil이 아닐 때, l1이 l2보다 작으면, output이 될 List에 l1.Val를 집어넣고, l1.Val가 추가된 인덱스의 l1을 l1.Next로 덮어써버림
    - 마찬가지로 l1과 l2가 모두 nil이 아닐 때, l2가 l1보다 작으면, l2.Val를 output에 추가, 역시 가장 앞에 있던 l2는 이제 l2.Next로 덮어씀
    - 만약 l1이나 l2가 다 땡겨져서 nil인 경우는 그대로 output에 추가하고, 한칸씩 땡긴다.
    - l1랑 l2가 둘 다 nil이 되면 작업을 끝냄
- LeetCode 통과
