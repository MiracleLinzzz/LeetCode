## Add One Row to Tree

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def addOneRow(self, root: Optional[TreeNode], val: int, depth: int) -> Optional[TreeNode]:
        if depth == 1:
            newRoot = TreeNode(val)
            newRoot.left = root
            return newRoot
        

        stack = [root]
        count = 0
        while stack:
            size = len(stack)
            count += 1
            for i in range(size):
                node = stack.pop(0)
                if count == depth-1:
                    templeft = node.left
                    node.left = TreeNode(val)
                    node.left.left = templeft
                    tempright = node.right
                    node.right = TreeNode(val)
                    node.right.right = tempright
                else:
                    if node.left:
                        stack.append(node.left)
                    if node.right:
                        stack.append(node.right)
        return root

```