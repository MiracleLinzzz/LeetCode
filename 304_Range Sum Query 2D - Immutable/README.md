## Range Sum Query 2D - Immutable

```
class NumMatrix:

    def __init__(self, matrix: List[List[int]]):
        self.preSum = matrix
        for row in range(1, len(matrix)):
            self.preSum[row][0] = matrix[row][0] + self.preSum[row-1][0]
        for col in range(1, len(matrix[0])):
            self.preSum[0][col] = matrix[0][col] + self.preSum[0][col-1]
        for row in range(1, len(matrix)):
            for col in range(1, len(matrix[0])):
                self.preSum[row][col] = matrix[row][col] + self.preSum[row-1][col] + self.preSum[row][col-1] - self.preSum[row-1][col-1]

    def sumRegion(self, row1: int, col1: int, row2: int, col2: int) -> int:
        return self.preSum[row2][col2] - (self.preSum[row2][col1-1] if col1 > 0 else 0) - (self.preSum[row1-1][col2] if row1 > 0 else 0) + (self.preSum[row1-1][col1-1] if row1 > 0 and col1 > 0 else 0)



# Your NumMatrix object will be instantiated and called as such:
# obj = NumMatrix(matrix)
# param_1 = obj.sumRegion(row1,col1,row2,col2)
```