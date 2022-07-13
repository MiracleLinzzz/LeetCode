## Search in a Binary Search Tree

### 递归方式

```
class Solution:
    def searchBST(self, root: TreeNode, val: int) -> TreeNode:
        if not root:
            return 

        if root.val > val:
            return self.searchBST(root.left, val)
        if root.val < val:
            return self.searchBST(root.right, val)
        
        return root
```

### 迭代方式
```
class Solution:
    def searchBST(self, root: TreeNode, val: int) -> TreeNode:

        while root:
            if root.val == val:
                return root
            elif root.val > val:
                root = root.left
            elif root.val < val:
                root = root.right
        return None
```