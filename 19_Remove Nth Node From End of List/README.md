## Remove Nth Node From End of List

快慢指针

```
class Solution:
    def removeNthFromEnd(self, head: ListNode, n: int) -> ListNode:
        dummy = ListNode(-1)
        dummy.next = head
        fast = dummy
        for i in range(n+1):
            fast = fast.next
        slow = dummy
        while fast:
            fast = fast.next
            slow = slow.next
        temp = slow.next
        slow.next = temp.next
        return dummy.next
```

or

```
class Solution:
    def removeNthFromEnd(self, head: ListNode, n: int) -> ListNode:
        dummy = ListNode(-1)
        dummy.next = head
        fast = dummy
        for i in range(n):
            fast = fast.next
        slow = dummy
        while fast.next:
            fast = fast.next
            slow = slow.next
        temp = slow.next
        slow.next = temp.next
        return dummy.next
        
```