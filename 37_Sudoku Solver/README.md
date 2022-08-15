## Sudoku Solver

```
class Solution:
    def solveSudoku(self, board: List[List[str]]) -> None:
        """
        Do not return anything, modify board in-place instead.
        """
        def backtrack(board, i, j):
            m = 9
            n = 9
            if j == n:
                return backtrack(board, i+1, 0)
            
            if i == m:
                return True
            
            if board[i][j] != '.':
                return backtrack(board, i, j+1)
            
            for char in range(1, 10):
                if not isValid(board, i, j, str(char)):
                    continue
                
                board[i][j] = str(char)

                if backtrack(board, i, j+1):
                    return True
                
                board[i][j] = '.'
            
            return False

        def isValid(board, r, c, n):
            for i in range(9):
                if board[r][i] == n: return False
                if board[i][c] == n: return False
                if board[(r//3)*3+i//3][(c//3)*3+i%3] == n:
                    return False
            return True
        
        return backtrack(board, 0, 0)
```