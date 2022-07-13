# Serialize and Deserialize Binary Tree

JSON 的运用非常广泛，比如我们经常将变成语言中的结构体序列化成 JSON 字符串，存入缓存或者通过网络发送给远端服务，消费者接受 JSON 字符串然后进行反序列化，就可以得到原始数据了。这就是「序列化」和「反序列化」的目的，以某种固定格式组织字符串，使得数据可以独立于编程语言。

那么假设现在有一棵用 Java 实现的二叉树，我想把它序列化字符串，然后用 C++ 读取这棵并还原这棵二叉树的结构，怎么办？这就需要对二叉树进行「序列化」和「反序列化」了。

**归根到底，是遍历与构造二叉树的过程**
由于我们有null标识符，所以通过一个遍历结果就可以还原出树的结构

### DFS

```
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Codec:

    def serialize(self, root):
        """Encodes a tree to a single string.
        
        :type root: TreeNode
        :rtype: str
        """
        def traverse(root):
            if not root:
                result.append("#")
                return 
            
            result.append(str(root.val))
            traverse(root.left)
            traverse(root.right)

        result = []
        traverse(root)
        return ",".join(result)
        


    def deserialize(self, data):
        """Decodes your encoded data to tree.
        
        :type data: str
        :rtype: TreeNode
        """
        def traverse(nodes):
            if not nodes:
                return
            first = nodes.pop()
            if first == "#":
                return 
            root = TreeNode(int(first))

            root.left = traverse(nodes)
            root.right = traverse(nodes)
        
            return root
        nodes = data.split(",")
        nodes.reverse()
        return traverse(nodes)
        

# Your Codec object will be instantiated and called as such:
# ser = Codec()
# deser = Codec()
# ans = deser.deserialize(ser.serialize(root))
```

或者

```
class Codec:

    def serialize(self, root):
        """Encodes a tree to a single string.
        
        :type root: TreeNode
        :rtype: str
        """
        if not root:
            return "#"

        return str(root.val) + "," + self.serialize(root.left) + "," + self.serialize(root.right)
        

    def deserialize(self, data):
        """Decodes your encoded data to tree.
        
        :type data: str
        :rtype: TreeNode
        """
        def traverse(nodes):
            if not nodes:
                return 
            rootVal = nodes.pop()
            if rootVal == "#":
                return 
            root = TreeNode(rootVal)
            root.left = traverse(nodes)
            root.right = traverse(nodes)
            return root
        
        nodes = data.split(",")
        nodes.reverse()
        return traverse(nodes)
```

### BFS
```
    def serialize(self, root):
        """Encodes a tree to a single string.
        
        :type root: TreeNode
        :rtype: str
        """
        if not root:
            return ""
        queue = collections.deque([root])
        res = []
        while queue:
            node = queue.popleft()
            if node:
                res.append(str(node.val))
                queue.append(node.left)
                queue.append(node.right)
            else:
                res.append('None')
        return '[' + ','.join(res) + ']'



        

    def deserialize(self, data):
        """Decodes your encoded data to tree.
        
        :type data: str
        :rtype: TreeNode
        """
        if not data:
            return []
        dataList = data[1:-1].split(',')
        root = TreeNode(int(dataList[0]))
        queue = collections.deque([root])
        i = 1
        while queue:
            node = queue.popleft()
            if dataList[i] != 'None':
                node.left = TreeNode(int(dataList[i]))
                queue.append(node.left)
            i += 1
            if dataList[i] != 'None':
                node.right = TreeNode(int(dataList[i]))
                queue.append(node.right)
            i += 1
        return root
```