## Corporate Flight Bookings

```
class Solution:
    def corpFlightBookings(self, bookings: List[List[int]], n: int) -> List[int]:
        totalBookings = [0 for _ in range(n)]

        for booking in bookings:
            totalBookings[booking[0]-1] += booking[2]
            if booking[1] < n:
                totalBookings[booking[1]] -= booking[2]
        
        for i in range(1, n):
            totalBookings[i] = totalBookings[i] + totalBookings[i-1]
        
        return totalBookings
```