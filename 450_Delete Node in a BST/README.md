## Delete Node in a BST

```
class Solution:
    def deleteNode(self, root: Optional[TreeNode], key: int) -> Optional[TreeNode]:

        def getMin(root):
            while root.left:
                root = root.left
            return root
        
        if not root:
            return 
        if root.val == key:
            if not root.left: return root.right
            if not root.right: return root.left
            candidate = getMin(root.right)
            root.right = self.deleteNode(root.right, candidate.val)
            candidate.left = root.left
            candidate.right = root.right
            root = candidate
            return root
        elif root.val > key:
            root.left = self.deleteNode(root.left, key)
        elif root.val < key:
            root.right = self.deleteNode(root.right, key)
        
        return root
```