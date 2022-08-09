## Interval List Intersections

```
class Solution:
    def intervalIntersection(self, firstList: List[List[int]], secondList: List[List[int]]) -> List[List[int]]:
        m = len(firstList)
        n = len(secondList)
        first = 0
        second = 0
        result = []
        while first < m and second < n:
            a1 = firstList[first][0]
            a2 = firstList[first][1]
            b1 = secondList[second][0]
            b2 = secondList[second][1]

            if a2 >= b1 and b2 >= a1:
                result.append([max(a1, b1), min(a2, b2)])
            
            if a2 < b2:
                first += 1
            else:
                second += 1

        return result 

```