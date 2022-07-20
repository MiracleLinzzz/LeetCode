## Range Sum Query - Immutable

前缀和数组

```
class NumArray:

    def __init__(self, nums: List[int]):
        self.preSum = [0 for _ in range(len(nums))]
        self.preSum[0] = nums[0]
        for idx in range(1, len(nums)):
            self.preSum[idx] = self.preSum[idx-1] + nums[idx]

    def sumRange(self, left: int, right: int) -> int:
        return self.preSum[right] - (self.preSum[left-1] if left > 0 else 0)


# Your NumArray object will be instantiated and called as such:
# obj = NumArray(nums)
# param_1 = obj.sumRange(left,right)
```