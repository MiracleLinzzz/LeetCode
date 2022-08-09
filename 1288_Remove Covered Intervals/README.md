## Remove Covered Intervals

```
class Solution:
    def removeCoveredIntervals(self, intervals: List[List[int]]) -> int:
        intervals.sort(key=lambda x: (x[0], -x[1]))
        right = intervals[0][1]
        result = 0
        n = len(intervals)
        for i in range(1, n):
            if intervals[i][1] <= right:
                result += 1
            else:
                right = intervals[i][1]
        return n - result
```