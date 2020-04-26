####
####

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

func addTwoNumbers(l1 *ListNode, l2 *ListNode) *ListNode {
	output := &List{}

	var quotient int
	var remainder int
	var temp int
	for l1 != nil || l2 != nil {
		switch {
		case l1 != nil && l2 != nil:
			temp = l1.Val + l2.Val + quotient
			remainder = temp % 10
			output.push(remainder)
			quotient = temp / 10
			l1 = l1.Next
			l2 = l2.Next
		case l1 != nil && l2 == nil:
			temp = l1.Val + quotient
			remainder = temp % 10
			output.push(remainder)
			quotient = temp / 10
			l1 = l1.Next
		case l1 == nil && l2 != nil:
			temp = l2.Val + quotient
			remainder = temp % 10
			output.push(remainder)
			quotient = temp / 10
			l2 = l2.Next
		}
	}
	if quotient != 0 {
		output.push(quotient)
	}
	n := output.first()

    return n
}
```
