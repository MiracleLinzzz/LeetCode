## Invert Binary Tree

1、这题能不能用「遍历」的思维模式解决？

可以，我写一个 traverse 函数遍历每个节点，让每个节点的左右子节点颠倒过来就行了。

单独抽出一个节点，需要让它做什么？让它把自己的左右子节点交换一下。

需要在什么时候做？好像前中后序位置都可以。

```
class Solution:
    def invertTree(self, root: TreeNode) -> TreeNode:

        def traverse(root):
            if not root:
                return
            
            temp = root.left
            root.left = root.right
            root.right = temp

            traverse(root.left)
            traverse(root.right)

        traverse(root)
        return root
```


2、这题能不能用「分解问题」的思维模式解决？

我们尝试给 invertTree 函数赋予一个定义：
```
// 定义：将以 root 为根的这棵二叉树翻转，返回翻转后的二叉树的根节点
def invertTree(self, root: TreeNode);
```
然后思考，对于某一个二叉树节点 x 执行 invertTree(x)，你能利用这个递归函数的定义做点啥？

我可以用 invertTree(x.left) 先把 x 的左子树翻转，再用 invertTree(x.right) 把 x 的右子树翻转，最后把 x 的左右子树交换，这恰好完成了以 x 为根的整棵二叉树的翻转，即完成了 invertTree(x) 的定义。

这种「分解问题」的思路，核心在于你要给递归函数一个合适的定义，然后用函数的定义来解释你的代码；如果你的逻辑成功自恰，那么说明你这个算法是正确的。
```
class Solution:
    def invertTree(self, root: TreeNode) -> TreeNode:

        if not root:
            return 

        left = self.invertTree(root.left)
        right = self.invertTree(root.right)

        root.right = left
        root.left = right

        return root
```