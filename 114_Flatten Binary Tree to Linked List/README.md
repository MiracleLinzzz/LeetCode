## Flatten Binary Tree to Linked List

### 分解子问题
```
class Solution:
    def flatten(self, root: TreeNode) -> None:
        """
        Do not return anything, modify root in-place instead.
        """
        if not root:
            return 

        self.flatten(root.left)
        self.flatten(root.right)

        left = root.left
        right = root.right

        root.left = None
        root.right = left

        temp = root
        while temp.right:
            temp = temp.right
        temp.right = right
```