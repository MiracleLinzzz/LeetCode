## Reverse Linked List II

```
class Solution:
    successor = ListNode(None)
    def reverseBetween(self, head: ListNode, left: int, right: int) -> ListNode:

        def reverse(head: ListNode, count: int):
            if not head or not head.next or count == 1:
                self.successor = head.next
                return head
            
            last = reverse(head.next, count-1)
            head.next.next = head
            head.next = self.successor
            return last
        
        if left == 1:
            return reverse(head, right)
        head.next = self.reverseBetween(head.next, left-1, right-1)
        return head
    ```