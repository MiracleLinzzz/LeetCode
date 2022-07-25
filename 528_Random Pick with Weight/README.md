## Random Pick with Weight




```
import random
class Solution:

    def __init__(self, w: List[int]):
        self.preSum = [0 for _ in range(len(w)+1)]
        for i in range(0, len(w)):
            self.preSum[i+1] = self.preSum[i] + w[i]

    def pickIndex(self) -> int:
        rand = random.randint(1,self.preSum[-1])
        # print(self.preSum, rand)
        left, right = 0, len(self.preSum)
        while left < right:
            mid = left + (right-left) // 2
            if self.preSum[mid] == rand:
                right = mid
            elif self.preSum[mid] > rand:
                right = mid
            elif self.preSum[mid] < rand:
                left = mid + 1
        return left-1



# Your Solution object will be instantiated and called as such:
# obj = Solution(w)
# param_1 = obj.pickIndex()
```