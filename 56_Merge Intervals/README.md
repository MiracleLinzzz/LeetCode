## Merge Intervals

```
class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        intervals.sort()
        result = [intervals[0]]
        n = len(intervals)
        for i in range(1, n):
            cur = intervals[i]
            last = result[-1]
            if cur[0] <= last[1]:
                last[1] = max(last[1], cur[1])
            else:
                result.append(cur)
        return result
```