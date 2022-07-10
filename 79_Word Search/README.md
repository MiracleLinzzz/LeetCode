## Word Search

### 说明：

1. 偏移量数组在二维平面内是经常使用的，可以把它的设置当做一个技巧，并且在这个问题中，偏移量数组内的 4 个偏移的顺序无关紧要；
说明：类似使用这个技巧的问题还有：「力扣」第 130 题：被围绕的区域、「力扣」第 200 题：岛屿数量。

2. 对于这种搜索算法，我认为理解 DFS 和状态重置并不难，代码编写也相对固定，难在代码的编写和细节的处理，建议多次编写，自己多总结多思考，把自己遇到的坑记下。

我自己在写

```
for i in range(m):
    for j in range(n):
        # 对每一个格子都从头开始搜索
        if self.__search_word(board, word, 0, i, j, marked, m, n):
            return True
```
这一段的时候，就写成了：

```
# 这一段代码是错误的，不要模仿
for i in range(m):
    for j in range(n):
        # 对每一个格子都从头开始搜索
        return self.__search_word(board, word, 0, i, j, marked, m, n)
```

这样其实就变成只从坐标 (0,0) 开始搜索，搜索不到返回 False，但题目的意思是：只要你的搜索返回 True 才返回，如果全部的格子都搜索完了以后，都返回 False ，才返回 False。

```
class Solution:
    def exist(self, board: List[List[str]], word: str) -> bool:
        def inRange(x: int, y: int):
            return x >= 0 and x < m and y >= 0 and y < n
    

        def dfs(row: int, col: int, start: int):
            # print(start, row, col, visited)
            if start == len(word) - 1:
                return board[row][col] == word[start]
            
            if board[row][col] == word[start]:
                visited[row][col] = 1
                for x, y in DIRECTIONS:
                    newRow, newCol = row+x, col+y
                    if inRange(newRow, newCol) and visited[newRow][newCol] == 0:
                        if dfs(newRow, newCol, start+1) :
                            return True
                visited[row][col] = 0
            return False

        DIRECTIONS = [(-1, 0), (0, -1), (0, 1), (1, 0)]
        m = len(board)
        n = len(board[0])
        # visited = [[0] * n] * m 引以为戒
        visited = [[0 for _ in range(n)] for _ in range(m)]
        for i in range(m):
            for j in range(n):
                if dfs(i, j, 0):
                    return True
        return False

        
```