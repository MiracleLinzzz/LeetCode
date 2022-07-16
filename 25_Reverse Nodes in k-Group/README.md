## Reverse Nodes in k-Group

困难问题是简单问题的集合与进阶  
解决困难问题需要先抽离出简单问题的模型

以k为单位反转链表的思考步骤

1. 此前已经写过了翻转整体链表的代码  
可以看做是从结点a到none的翻转
```
def reverse(head: Optional[ListNode]) -> Optional[ListNode]:
    pre = None
    cur = head
    nxt = head
    while cur:
        nxt = cur.next
        cur.next = pre
        pre = cur
        cur = nxt
    return pre
```

2. 那么从结点a到结点b的翻转就顺理成章为  
更改一下结束判断

```
def reverse(head: Optional[ListNode], end: Optional[ListNode]) -> Optional[ListNode]:
    pre = None
    cur = head
    nxt = head
    while cur != end:
        nxt = cur.next
        cur.next = pre
        pre = cur
        cur = nxt
    return pre
```

3. 递归完成各个从a到b的翻转子过程

```
def reverseKGroup(self, head: Optional[ListNode], k: int) -> Optional[ListNode]:
    def reverse(head: Optional[ListNode], end: Optional[ListNode]) -> Optional[ListNode]:
        pre = None
        cur = head
        nxt = head
        while cur != end:
            nxt = cur.next
            cur.next = pre
            pre = cur
            cur = nxt
        return pre
    start = head
    end = head
    for _ in range(k):
        if not end: return head
        end = end.next
    newHead = reverse(start, end)
    start.next = self.reverseKGroup(end, k)
    return newHead
```

4. 整体都是迭代

```
def reverseKGroup(self, head: Optional[ListNode], k: int) -> Optional[ListNode]:
    # 先实现反转整个链表 迭代方法
    def reverse(head: Optional[ListNode], tail: Optional[ListNode]) -> Optional[ListNode]:
        pre = tail.next
        cur = head
        nxt = head
        while pre != tail:
            nxt = cur.next
            cur.next = pre
            pre = cur
            cur = nxt
        return tail, head
    
    dummy = ListNode(-1)
    dummy.next = head
    pre = dummy
    tail = dummy
    while head:
        for _ in range(k):
            if not tail.next: return dummy.next
            tail = tail.next
        nxt = tail.next
        pre.next, tail = reverse(head, tail)
        pre = tail
        head = nxt
        
    return dummy.next
```