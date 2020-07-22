#### Reverse Linked List
#### Writer: Haram Ryu
#### Refer: LeetCode

## 문제 설명
Singly linked list가 주어지는데 순서를 거꾸로 바꾸어서 출력한다
***예시***
```
Input: 1->2->3->4->5->nil
Output: 5->4->3->2->1->nil
```
- iterative한 방법과 recursive한 방법을 둘 다 적용해보자
## 솔루션1-iterative
```
func reverseList(head *ListNode) *ListNode {
    curr := head
    var rev *ListNode
    for curr != nil {
        nextTemp := curr.Next
        curr.Next = rev
        rev = curr
        curr = nextTemp
    }
    return rev
}
```
- 변수는 세개를 사용
    - curr: 처음에는 입력값을 받고, 앞에거부터 하나씩 떼어주는 포인터
    - nextTemp: 입력값에서 하나씩 떼어진 나머지를 임시 보관
    - rev: 거꾸로 바뀌게 될 결과값을 저장
- 과정은 그림으로 설명
## 솔루션2-recursive
```
func reverseList(head *ListNode) *ListNode {
    if head == nil || head.Next == nil {
        return head
    }
    ret := reverseList(head.Next)
    head.Next.Next = head
    head.Next = nil
    return ret
}
```
- 재귀적으로 풀 때는 가장 마지막 노드를 찾아 들어가서 이전 노드를 바라보게 하고, 가장 마지막 노드의 포인터를 반환한다
- 과정은 그림으로 설명
## 종합
- 이 아이디어를 어떻게 생각해내야하는지..
