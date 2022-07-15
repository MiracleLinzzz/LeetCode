## Merge Two Sorted Lists

```
class Solution:
    def mergeTwoLists(self, list1: Optional[ListNode], list2: Optional[ListNode]) -> Optional[ListNode]:
        point1 = list1
        point2 = list2
        temp = ListNode(-1)
        result = temp
        while point1 and point2:
            if point1.val > point2.val:
                temp.next = point2
                point2 = point2.next
            else:
                temp.next = point1
                point1 = point1.next
            temp = temp.next
        
        if point1:
            temp.next = point1
        elif point2:
            temp.next = point2
        
        return result.next
```