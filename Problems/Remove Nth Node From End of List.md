#### Remove Nth Node From End of List
#### Writer: Haram Ryu
#### Refer: LeetCode

## 문제 설명
주어진 링크드 리스트에서 끝에서부터 n번째 노드를 제거하고나서 헤드를 반환하면 됨  

***예시***
```
입력: 1->2->3->4->5, n=2
끝에서 두번째 노드를 제거, 1->2->3->5를 리턴
```

## 솔루션
```
변수
var deleteNode *ListNode = head  
var prevNode *ListNode = deleteNode  
var indexNode *ListNode = head  
var distance int = 1  
var length = 0  
```
- deleteNode: 지워져야 할 노드
- distance: indexNode와 deleteNode와의 거리를 저장
    - distance가 n보다 작을때는 indexNode만 넘기면서 distance가 증가
    - distance가 n이 되면 indexNode와 deleteNode를 함께 넘김
- prevNode: deleteNode를 넘기기 직전에 deleteNode를 저장하여 deleteNode의 이전 값 저장
- length: 링크드 리스트의 길이를 저장. 0과 1일 경우에 대해서만 특별한 처리가 필요. 최종적인 length의 결정은 indexNode.Next == nil일 때 length의 증가를 멈추면서 결정.

```
// 삭제해야할 노드를 찾는 for문
	for {

		if distance < n && indexNode.Next != nil {
			indexNode = indexNode.Next
			length++
			distance++
			continue
		}

		if indexNode.Next == nil {
			break
		}

		prevNode = deleteNode
		deleteNode = deleteNode.Next
		indexNode = indexNode.Next
		length++

	}
  
  // 찾은 deleteNode에 대하여 처리
  
  // 먼저 length가 0인 경우는 노드가 한개 밖에 없는 경우
  	if length == 0 {
		return nil
	}
  
  // deleteNode가 선언한 head에 머물러 있다는 것은 indexNode만 증가했다는 뜻
    if deleteNode == head {
        return deleteNode.Next
    }
    
  // 삭제할 노드의 이전 노드의 Next 포인터를 삭제할 노드의 Next 포인터로 대체하는 것이 삭제  
	prevNode.Next = deleteNode.Next

	return head

```
## 제출 결과
- 통과됐고, 원패스로 하라는 조건도 충족
