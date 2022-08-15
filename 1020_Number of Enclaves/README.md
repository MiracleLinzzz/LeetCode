## Number of Enclaves

和1254一样 两种思路  
1. 先淹了边界的
2. 加一个边界逻辑判断

```
class Solution:
    def numEnclaves(self, grid: List[List[int]]) -> int:

        def dfs(grid, i, j):
            if i < 0 or j < 0 or i == m or j == n:
                return 
            if grid[i][j] == 0:
                return 
            
            grid[i][j] = 0
            dfs(grid, i+1, j)
            dfs(grid, i-1, j)
            dfs(grid, i, j+1)
            dfs(grid, i, j-1)
        
        m = len(grid)
        n = len(grid[0])
        for i in range(m):
            dfs(grid, i, 0)
            dfs(grid, i, n-1)
        for j in range(n):
            dfs(grid, 0, j)
            dfs(grid, m-1, j)
        result = 0
        for i in range(1, m-1):
            for j in range(1, n-1):
                if grid[i][j] == 1:
                    result += 1
        return result
```