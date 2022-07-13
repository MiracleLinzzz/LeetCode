## Validate Binary Search Tree

```
class Solution:
    def isValidBST(self, root: Optional[TreeNode]) -> bool:

        def traverse(root: Optional[TreeNode], minimum: int, maximum: int):
            if not root:
                return True

            if minimum != None and minimum >= root.val:
                return False
            if maximum != None and maximum <= root.val:
                return False
            
            return traverse(root.left, minimum, root.val) and traverse(root.right, root.val, maximum)
        
        return traverse(root, None, None)
```