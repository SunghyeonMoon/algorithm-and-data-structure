# [Leetcode] 203. [Remove Linked List Elements](https://leetcode.com/problems/remove-linked-list-elements/)

현재 노드가 찾는값이면 이전 노드에서 삭제
단, 현재 노드가 Head 노드일 때 이전 노드가 존재하지 않으므로 Head 노드 앞에 dummy 노드 생성

```py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def removeElements(self, head: Optional[ListNode], val: int) -> Optional[ListNode]:
        dummy = ListNode(None)
        dummy.next, curr, prev = head, head, dummy
        while curr:
            if curr.val == val:
                curr, prev.next = curr.next, curr.next
            else:
                prev, curr = curr, curr.next
        return dummy.next
```
