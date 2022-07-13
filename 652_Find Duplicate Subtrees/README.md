## Find Duplicate Subtrees

```
class Solution:
    def findDuplicateSubtrees(self, root: Optional[TreeNode]) -> List[Optional[TreeNode]]:

        def traverse(root):
            if not root:
                return '#'

            left = traverse(root.left)
            right = traverse(root.right)

            subTree = left + "," + right + "," + str(root.val)
            
            if subTree in subTrees:
                if subTrees[subTree] == 1:
                   result.append(root)
                   subTrees[subTree] += 1
            else:            
                subTrees[subTree] = 1
            # print(subTree, subTrees, root, result)
            return subTree
            
        subTrees = {}
        result = []
        traverse(root)
        return result
```