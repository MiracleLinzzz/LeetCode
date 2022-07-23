## Car Pooling

```
class Solution:
    def carPooling(self, trips: List[List[int]], capacity: int) -> bool:
        car = [0 for _ in range(1001)]

        for trip in trips:
            car[trip[1]] += trip[0]
            car[trip[2]] -= trip[0]
        print(car)
        for idx in range(1000):
            car[idx] = car[idx] + car[idx-1] if idx>0 else car[idx]
            if car[idx] > capacity:
                return False
        
        return True
```