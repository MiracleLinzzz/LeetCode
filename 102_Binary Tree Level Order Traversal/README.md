## Binary Tree Level Order Traversal

```
from collections import deque
class Solution:
    def levelOrder(self, root: TreeNode) -> List[List[int]]:

        if not root:
            return []
        result = []
        stack = deque()
        stack.append(root)
        while stack:
            size = len(stack)
            temp = []
            for i in range(size):
                node = stack.popleft()
                temp.append(node.val)
                if node.left:
                    stack.append(node.left)
                if node.right:
                    stack.append(node.right)
            result.append(temp)
            
        return result
```