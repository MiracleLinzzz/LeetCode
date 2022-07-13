## Binary Search Tree to Greater Sum Tree
BST 的特性：

1、对于 BST 的每一个节点 node，左子树节点的值都比 node 的值要小，右子树节点的值都比 node 的值大。

2、对于 BST 的每一个节点 node，它的左侧子树和右侧子树都是 BST。

二叉搜索树并不算复杂，但我觉得它可以算是数据结构领域的半壁江山，直接基于 BST 的数据结构有 AVL 树，红黑树等等，拥有了自平衡性质，可以提供 logN 级别的增删查改效率；还有 B+ 树，线段树等结构都是基于 BST 的思想来设计的。


**从做算法题的角度来看 BST，除了它的定义，还有一个重要的性质：BST 的中序遍历结果是有序的（升序）。**

也就是说，如果输入一棵 BST，以下代码可以将 BST 中每个节点的值升序打印出来：
```
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    Add = 0
    def bstToGst(self, root: TreeNode) -> TreeNode:
        

        def traverse(root):
            if not root:
                return 

            traverse(root.right)           
            self.Add += root.val
            root.val = self.Add
            traverse(root.left)


        traverse(root)
        return root

```