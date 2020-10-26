### Print Immutable Linked List in Reverse
#### Writer: Hyungjune Shin
#### Refer: LeetCode#1265
* * *
### Problem
다음의 인터페이스를 통하여 주어진 immutable linked list가 있을 때 역 방향으로 모든 노드의 값을 출력하는 문제입니다. 
  - ``ImmutableListNode:`` immutable linked list의 인터페이스입니다. 해당 리스트의 head가 주어집니다.
  
 linked list에 접근하기 위해 다음의 함수를 사용해야합니다. (``ImmutableListNode``를 직접 접근하지 마세요)
  - ``ImmutableListNode.printValue():`` 현재 노드의 값을 출력합니다.
  - ``ImmutableListNode.getNext():`` 다음 노드를 반환합니다.
  
linked list가 내부적으로 초기화된 입력 값이 주어집니다. linked list를 수정하면 안됩니다. 다시 말하면, 언급된 API들만 이용하여 문제를 풀어야 합니다.

<b>Example 1:</b>
<pre>
<b>Input:</b> head = [1,2,3,4]
<b>Output:</b> [4,3,2,1]
</pre>

<b>Example 2:</b>
<pre>
<b>Input:</b> head = [0,-4,-1,3,-5]
<b>Output:</b> [-5,3,-1,-4,-0]
</pre>

<b>Example 3:</b>
<pre>
<b>Input:</b> head = [-2,0,6,4,4,-6]
<b>Output:</b> [-6,4,4,6,0,-2]
</pre>

### Constrains: ###
  - linked list의 길이는 ``[1, 1000]`` 입니다.
  - linked list에 있는 노드의 값의 범위는 ``[-1000, 1000]`` 입니다.
  
* * *
### Solution
```go
/*   Below is the interface for ImmutableListNode, which is already defined for you.
 *
 *   type ImmutableListNode struct {
 *       
 *   }
 *
 *   func (this *ImmutableListNode) getNext() ImmutableListNode {
 *		// return the next node.
 *   }
 *
 *   func (this *ImmutableListNode) printValue() {
 *		// print the value of this node.
 *   }
 */

func printLinkedListInReverse(head ImmutableListNode) {
    if head.getNext() == nil {
        head.printValue()
    } else {
        printLinkedListInReverse(head.getNext())
        head.printValue()
    }
}
```

- 재귀함수를 통하여 가장 마지막 노드까지 간 뒤 함수를 나오면서 출력하면 됩니다.
