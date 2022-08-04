## Sum of Left Leaves

```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def sumOfLeftLeaves(self, root: Optional[TreeNode]) -> int:

        def traverse(root):
            if not root:
                return 
            
            left = traverse(root.left)
            right = traverse(root.right)
            if left and not left.left and not left.right:
                self.result += left.val
            
            return root
        
        self.result = 0
        traverse(root)
        return self.result
```