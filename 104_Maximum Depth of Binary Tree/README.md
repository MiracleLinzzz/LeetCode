## Maximum Depth of Binary Tree
利用二叉树的后序遍历  
可以很快得到子树的相关数据 进行计算  
**分解问题式**
```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:

        if not root:
            return 0
        
        maxLeftDepth = self.maxDepth(root.left)
        maxRightDepth = self.maxDepth(root.right)

        result = max(maxLeftDepth, maxRightDepth)

        return result + 1
        
```