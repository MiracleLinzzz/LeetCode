## Spiral Matrix


![](example.png)

不断坍缩
```
class Solution:
    def spiralOrder(self, matrix: List[List[int]]) -> List[int]:
        m = len(matrix)
        n = len(matrix[0])
        up, down = 0, m-1
        left, right = 0, n-1
        result = []
        while(len(result) < m*n):
            if up <= down:
                for i in range(left, right+1):
                    result.append(matrix[up][i])
                up += 1
            if left <= right:
                for i in range(up, down+1):
                    result.append(matrix[i][right])
                right -= 1
            if up <= down:
                for i in range(right, left-1, -1):
                    result.append(matrix[down][i])
                down -= 1
            if left <= right:
                for i in range(down, up-1, -1):
                    result.append(matrix[i][left])
                left += 1
        return result
```