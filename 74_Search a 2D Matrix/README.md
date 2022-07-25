## Search a 2D Matrix

```
class Solution:
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        rowIdx = 0
        for row in range(len(matrix)):
            if matrix[row][0] <= target:
                rowIdx = row

        left = 0
        right = len(matrix[0])
        while left < right:
            mid = left + (right-left) // 2
            if matrix[rowIdx][mid] == target:
                return True
            elif matrix[rowIdx][mid] > target:
                right = mid
            else:
                left = left + 1
        
        return False
```

### 也可以拉平成一位数组来做