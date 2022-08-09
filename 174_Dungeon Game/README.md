## Dungeon Game

转变dp定义

从左上角（grid[0][0]）走到 grid[i][j] 至少需要 dp(grid, i, j) 的生命值。

从 grid[i][j] 到达终点（右下角）所需的最少生命值是 dp(grid, i, j)。
```
class Solution:
    def calculateMinimumHP(self, dungeon: List[List[int]]) -> int:
        m = len(dungeon)
        n = len(dungeon[0])
        dp = [0] * (n+1)


        for i in range(m, -1, -1):
            for j in range(n, -1, -1):
                if i == m or j == n:
                    dp[j] = float('inf')
                    continue
                if i == m-1 and j == n-1:
                    dp[j] = -dungeon[i][j] + 1 if dungeon[i][j] <= 0 else 1
                    continue
                dp[j] = min(dp[j], dp[j+1]) - dungeon[i][j]
                if dp[j] <= 0:
                    dp[j] = 1
        return dp[0]
```