# [Leetcode] 876. Middle of the Linked List

2칸씩 움직이는 fast와 1칸씩 움직이는 slow를 이용해서 fast가 마지막 Node에 도달했을 때 slow 값을 반환

```py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def middleNode(self, head: Optional[ListNode]) -> Optional[ListNode]:
        fast = slow = head
        while fast.next and fast.next.next:
            fast, slow = fast.next.next, slow.next
        if fast.next:
            slow = slow.next
        return slow
```
