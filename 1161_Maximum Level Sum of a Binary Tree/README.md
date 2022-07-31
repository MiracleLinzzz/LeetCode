## Maximum Level Sum of a Binary Tree

### BFS层序遍历
```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def maxLevelSum(self, root: Optional[TreeNode]) -> int:
        stack = [root]
        layer = 1
        maxSum = float('-inf')
        while stack:
            size = len(stack)
            temp = 0
            for i in range(size):
                node = stack.pop(0)
                temp += node.val
                if node.left:
                    stack.append(node.left)
                if node.right:
                    stack.append(node.right)
            if maxSum < temp:
                result = layer
                maxSum = temp
            layer += 1
        return result
```

### 通过定义一个新的stack 实现了queue的效果 加速明显
```
class Solution:
    def maxLevelSum(self, root: Optional[TreeNode]) -> int:
        stack = [root]
        layer = 1
        maxSum = float('-inf')
        while stack:
            temp = 0
            newstack = []
            for node in stack:
                temp += node.val
                if node.left:
                    newstack.append(node.left)
                if node.right:
                    newstack.append(node.right)
            if maxSum < temp:
                result = layer
                maxSum = temp
            layer += 1
            stack = newstack
        return result
```