## Simplify Path

### 栈
- 运用栈对文件名进行划分  
- 算法题里能用split吗。。。

```
class Solution:
    def simplifyPath(self, path: str) -> str:
        stack = []
        name = ""
        for char in (path + "/"):
            if char == "/":
                if name == ".." and stack:
                    stack.pop()
                elif name and name != ".." and name != ".":
                    stack.append(name)
                name = ""
                continue
            name += char
            # print(stack)
        return "/" + "/".join(stack)
```