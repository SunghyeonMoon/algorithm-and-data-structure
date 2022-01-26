# [Leetcode] 141. [Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/)

## 1차 풀이

set을 활용한 풀이

```py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        node_set = set()
        node = head
        while node:
            if node in node_set:
                return True
            node_set.add(node)
            node = node.next
        return False
```

## 2차 풀이

루프가 있다면 fast와 slow가 만날 수 밖에 없다는 논리를 사용한 풀이

```py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        fast, slow = head, head
        while fast and fast.next:
            fast, slow = fast.next.next, slow.next
            if slow == fast:
                return True
        return False
```
