## Surrounded Regions

Union Find Search
并查集在这个题里面效率不高 但是可以作为模板练习
```
class Solution:
    def solve(self, board: List[List[str]]) -> None:
        if len(board) == 0:
            return 
        m = len(board)
        n = len(board[0])
        UF = UnionFind(m*n+1)
        dummy = m*n
        for i in range(m):
            if board[i][0] == 'O':
                UF.union(i*n, dummy)
            if board[i][n-1] == 'O':
                UF.union(i*n + n-1, dummy)
        
        for j in range(n):
            if board[0][j] == 'O':
                UF.union(j, dummy)
            if board[m-1][j] == 'O':
                UF.union(n*(m-1) + j, dummy)

        directions = [[1,0], [0,1], [0,-1], [-1,0]]
        for i in range(1, m-1):
            for j in range(1, n-1):
                if board[i][j] == 'O':
                    for k in range(4):
                        x = i+directions[k][0]
                        y = j+directions[k][1]
                        if board[x][y] == 'O':
                            UF.union(x*n+y, i*n+j)

        for i in range(1, m-1):
            for j in range(1, n-1):
                if not UF.connected(dummy, i*n+j):
                    board[i][j] = 'X'
 


class UnionFind:
    def __init__(self, nodeNum: int):
        self.count = nodeNum
        self.parent = [0 for _ in range(nodeNum)]
        for i in range(nodeNum):
            self.parent[i] = i
        
    def union(self, p, q):
        rootP = self.find(p)
        rootQ = self.find(q)

        if rootP == rootQ:
            return
        
        self.parent[rootQ] = rootP
        self.count -= 1

    def connected(self, p, q):
        rootP = self.find(p)
        rootQ = self.find(q)
        return rootP == rootQ

    def find(self, x: int):
        if self.parent[x] != x:
            self.parent[x] = self.find(self.parent[x])

        return self.parent[x]

    def count(self):
        return self.count
```

or

```
class Solution:
    def solve(self, board: List[List[str]]) -> None:
        """
        Do not return anything, modify board in-place instead.
        """
        f = {}
        def find(x):
            f.setdefault(x, x)
            if f[x] != x:
                f[x] = find(f[x])
            return f[x]
        def union(x, y):
            f[find(y)] = find(x)

            
            
        if not board or not board[0]:
            return
        row = len(board)
        col = len(board[0])
        dummy = row * col
        for i in range(row):
            for j in range(col):
                if board[i][j] == "O":
                    if i == 0 or i == row - 1 or j == 0 or j == col - 1:
                        union(i * col + j, dummy)
                    else:
                        for x, y in [(-1, 0), (1, 0), (0, -1), (0, 1)]:
                            if board[i + x][j + y] == "O":
                                union(i * col + j, (i + x) * col + (j + y))
        for i in range(row):
            for j in range(col):
                if find(dummy) == find(i * col + j):
                    board[i][j] = "O"
                else:
                    board[i][j] = "X"


```