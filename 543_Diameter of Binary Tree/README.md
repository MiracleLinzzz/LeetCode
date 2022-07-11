## Diameter of Binary Tree


**分解问题的思路**
```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    diameter = 0
    def diameterOfBinaryTree(self, root: Optional[TreeNode]) -> int:

        def traverse(root):
            if not root:
                return 0

            maxLeftDepth = traverse(root.left)
            maxRightDepth = traverse(root.right)

            maxDepth = max(maxLeftDepth, maxRightDepth)
            
            self.diameter = max(self.diameter, maxLeftDepth + maxRightDepth)

            return maxDepth + 1
        
        
        traverse(root)
        return self.diameter
```