## Number of Closed Islands

```
class Solution:
    def closedIsland(self, grid: List[List[int]]) -> int:

        def dfs(grid, i, j):
            if i < 0 or j < 0 or i == m or j == n:
                return False
            
            if grid[i][j] == 1:
                return True
            else:
                grid[i][j] = 1

                return dfs(grid, i+1, j) & \
                dfs(grid, i-1, j) & \
                dfs(grid, i, j+1) & \
                dfs(grid, i, j-1) 

        m = len(grid)
        n = len(grid[0])
        count = 0
        for i in range(m):
            for j in range(n):
                if grid[i][j] == 0:
                    if dfs(grid, i, j):
                        count += 1
        return count

```