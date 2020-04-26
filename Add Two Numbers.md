#### Add Two Numbers
#### Writer: Haram Ryu
#### Refer: LeetCode

## 문제 설명
음수가 아닌 두개의 정수가 두개의 비어있지 않은 linked list가 주어짐.  
각자릿수가 역순으로 linked list로 저장되어있음.  
두개의 숫자를 더해서 linked list로 반환하라.  

## 조건
- 맨 앞자리 수는 0으로 나오지 않음. 0인 경우를 제외하고.  
***예시***
```
Input: (2->4->3)+(5->6->4)
Output: 7->0->8
Explanation: 342 + 456 = 807
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
- Linked list를 사용하는 문제이고, l1, l2에서 꺼낼 때 일의 자리, 십의 자리, 백의 자리 순서로 나오기 때문에 연산 순서도 일의 자리, 십의 자리, 백의 자리 순서로 하게 된다.
    - 답안도 일의자리->십의자리->백의자리 이렇게 역순인 linked list로 제출하므로, 맨 뒤에 넣으려면 push()가 필요
- for 반복문은 l1과 l2가 모두 nil이 아닌 동안 반복한다.
    - 가장 기본적인 경우는 l1과 l2가 모두 nil이 아닌 경우
        - 1. 두 linked list의 head를 꺼내서 서로 더하고 거기에 이전 연산의 몫(quotient)까지 더한다. (l1.Val + l2.Val + quotient): 이게 temp에 저장됨
	- 2. temp를 10으로 나눈 나머지(remainder)를 output에 푸쉬
	- 3. temp를 10으로 나눴을 때 몫(quotient)은 다음 연산에서 temp를 만들 때 더해서 다음 자리수 연산에 반영
	- 4. 마지막에 l1과 l2를 한자리씩 앞으로 땡긴다
    - l1만 nil이 아닌 경우에는 l1의 모든 자리수를 output에 푸쉬하고, l2만 nil이 아닌 경우에도 마찬가지
    - for문이 다 끝난 후에도 즉, l1과 l2의 마지막 자리수 연산이 끝난 경우에도 10이 넘어갔으면 몫이 1이 남아있을 수 있는데, 그 경우에 output에 push하면서 계산 마무리
- LeetCode 통과 완료
