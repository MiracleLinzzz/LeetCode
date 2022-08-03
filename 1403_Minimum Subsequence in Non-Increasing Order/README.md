## Minimum Subsequence in Non-Increasing Order

```
class Solution:
    def minSubsequence(self, nums: List[int]) -> List[int]:
        if not nums:
            return []
        nums.sort(reverse = True)
        target = sum(nums)
        cur = 0
        index = 0
        for num in nums:
            cur += num
            index += 1
            if cur > target-cur:
                return nums[:index]
```