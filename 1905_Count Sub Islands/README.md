## Count Sub Islands

```
class Solution:
    def countSubIslands(self, grid1: List[List[int]], grid2: List[List[int]]) -> int:

        def dfs(grid, i, j):
            if i < 0 or j < 0 or i == m or j == n:
                return
            
            if grid[i][j] == 0:
                return 
            else:
                grid[i][j] = 0

                dfs(grid, i+1, j)
                dfs(grid, i-1, j)
                dfs(grid, i, j+1)
                dfs(grid, i, j-1)

        m = len(grid1)
        n = len(grid1[0])
        for i in range(m):
            for j in range(n):
                if grid1[i][j] == 0 and grid2[i][j] == 1:
                    dfs(grid2, i, j)
        
        result = 0
        for i in range(m):
            for j in range(n):
                if grid2[i][j] == 1:
                    result += 1
                    dfs(grid2, i, j)

        return result
```