## Middle of the Linked List

```
class Solution:
    def middleNode(self, head: ListNode) -> ListNode:
        fast = head
        slow = head

        while fast and fast.next:
            fast = fast.next.next
            slow = slow.next
        
        return slow
```