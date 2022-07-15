## Partition List

因为我们做的是分解一个链表到两个链表
需要断开原本node的next，否则出错
很奇怪的点是在没断开的时候 run超时了？
是有死循环吗还是其他？

```
class Solution:
    def partition(self, head: ListNode, x: int) -> ListNode:
        dummy1 = ListNode(-1)
        dummy2 = ListNode(-2)
        temp1 = dummy1
        temp2 = dummy2
        pointer = head
        while pointer:
            if pointer.val < x:
                temp1.next = pointer
                temp1 = temp1.next
            else:
                temp2.next = pointer
                temp2 = temp2.next
            pointer = pointer.next
            # temp = pointer.next   断开方法1
            # pointer.next = None
            # pointer = temp

        temp2.next = None   # 断开方法2
        temp1.next = dummy2.next
        return dummy1.next
```