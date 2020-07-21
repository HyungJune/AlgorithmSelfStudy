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
## 솔루션1

## 솔루션2
```
func reverseList(head *ListNode) *ListNode {
    curr := head
    var prev *ListNode
    for curr != nil {
        nextTemp := curr.Next
        curr.Next = prev
        prev = curr
        curr = nextTemp
    }
    return prev
}
```
