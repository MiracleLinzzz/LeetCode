## Insert into a Binary Search Tree

### 迭代
```
class Solution:
    def insertIntoBST(self, root: TreeNode, val: int) -> TreeNode:
        if not root:
            return TreeNode(val)
        result = root
        while root:
            if root.val > val:
                if root.left:
                    root = root.left
                else:
                    root.left = TreeNode(val)
                    break
            if root.val < val:
                if root.right:
                    root = root.right 
                else:
                    root.right = TreeNode(val)
                    break
        return result
```


### 递归
```
class Solution:
    def insertIntoBST(self, root: TreeNode, val: int) -> TreeNode:
        if not root:
            return TreeNode(val)

        if root.val > val:
            root.left = self.insertIntoBST(root.left, val)
        if root.val < val:
            root.right = self.insertIntoBST(root.right, val)
        return root
        
```