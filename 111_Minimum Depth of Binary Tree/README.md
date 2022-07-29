## Minimum Depth of Binary Tree

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def minDepth(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0
        stack = [root]
        depth = 1
        while stack:
            size = len(stack)
            for i in range(size):
                node = stack.pop(0)
                if not node.left and not node.right:
                    return depth
                if node.left:
                    stack.append(node.left)
                if node.right:
                    stack.append(node.right)
            depth += 1
        return depth
```