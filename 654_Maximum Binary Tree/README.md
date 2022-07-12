## Maximum Binary Tree



```
class Solution:
    def constructMaximumBinaryTree(self, nums: List[int]) -> TreeNode:
        if not nums:
            return

        rootVal = max(nums)
        rootIdx = nums.index(rootVal)

        root = TreeNode(rootVal)
        left = self.constructMaximumBinaryTree(nums[:rootIdx])
        right = self.constructMaximumBinaryTree(nums[rootIdx+1:])
        root.left = left
        root.right = right

        return root
```