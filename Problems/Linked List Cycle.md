### Linked List Cycle
#### Writer: Haram Ryu
#### Refer: LeetCode#141 (Easy)
* * *
### Problem
Given head, the head of a linked list, determine if the linked list has a cycle in it.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the next pointer. Internally, pos is used to denote the index of the node that tail's next pointer is connected to. Note that pos is not passed as a parameter.

Return true if there is a cycle in the linked list. Otherwise, return false.

<b>Example 1</b>
![image](https://user-images.githubusercontent.com/22101375/127859292-fbacc38e-dae2-41f4-9839-42d14432ad05.png)
<pre>
<b>Input</b>: head = [3,2,0,-4], pos = 1
<b>Output</b>: true
<b>Explanation</b>: There is a cycle in the linked list, where the tail connects to the 1st node (0-indexed).
</pre>

<b>Example 2</b>
![image](https://user-images.githubusercontent.com/22101375/127859483-5b31772f-a98b-4399-902d-2e957fc08a16.png)
<pre>
<b>Input</b>: head = [1,2], pos = 0
<b>Output</b>: true
<b>Explanation</b>: There is a cycle in the linked list, where the tail connects to the 0th node.
</pre>

<b>Example 2</b>
![image](https://user-images.githubusercontent.com/22101375/127859483-5b31772f-a98b-4399-902d-2e957fc08a16.png)
<pre>
<b>Input</b>: head = [1,2], pos = 0
<b>Output</b>: true
<b>Explanation</b>: There is a cycle in the linked list, where the tail connects to the 0th node.
</pre>

<b>Example 3</b>
![image](https://user-images.githubusercontent.com/22101375/127859556-e21fb538-da7a-494e-b3fd-dfbe30842456.png)
<pre>
<b>Input</b>: head = [1], pos = -1
<b>Output</b>: false
<b>Explanation</b>: There is no cycle in the linked list.
</pre>
#### Constraints
- The number of the nodes in the list is in the range [0, 104].
- -10^5 <= Node.val <= 10^5
- pos is -1 or a valid index in the linked-list.

### Solution
```golang
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func hasCycle(head *ListNode) bool {
    if head == nil {
        return false
    }

    slow := head.Next
    if slow == nil {
        return false
    }

    fast := slow.Next

    for fast != nil && slow != nil {
        if fast == slow {
            return true
        }

        slow = slow.Next
        
        fast = fast.Next
        if fast != nil {
            fast = fast.Next
        }
    }

    return false
}
}
```
- 
