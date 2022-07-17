## Array Nesting

本质上是求一个图的问题，结点一定会有环
求最大环的节点数

### DFS

```

def traverse(k):
    if visited[k] == 1:
        self.maxlength = max(self.maxlength, self.count)
        return 
    self.count += 1
    visited[k] = 1
    traverse(nums[k])

    
self.maxlength = 0
n = len(nums)
visited = [0 for _ in range(n)]
for i in range(n):
    if visited[i] == 1:
        continue
    self.count = 0
    traverse(i)
return self.maxlength
```

### 原地标记

```
def arrayNesting(self, nums: List[int]) -> int:
    ans, n = 0, len(nums)
    for i in range(n):
        cnt = 0
        while nums[i] < n:
            num = nums[i]
            nums[i] = n
            i = num
            cnt += 1
        ans = max(ans, cnt)
    return ans

```