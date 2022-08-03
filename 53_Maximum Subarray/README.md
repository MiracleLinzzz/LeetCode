## Maximum Subarray
**Kadane's algorithm**

dp[i]数组的定义不是nums[0:i]的最大和数组  
因为当前数字可能与前面最大和数组不连续  
所以定义可以改为以nums[i]为结尾的最大和数组  
所以要么就是和前面数组评起来 要么就是自成一派

**朴素动态O(N)**
```
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        n = len(nums)
        dp = [0 for _ in range(n)]
        dp[0] = nums[0]
        for i in range(1, n):
            dp[i] = max(nums[i], nums[i]+dp[i-1])
        return max(dp)
```

**由于当前状态只与前一个状态有关，所以可以把dp数组改成两个数来降低空间复杂度**
```
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        n = len(nums)
        cur = 0
        pre = nums[0]
        maxSum = pre //重点
        for i in range(1, n):
            cur = max(pre+nums[i], nums[i])
            if cur > maxSum:
                maxSum = cur
            pre = cur
        return maxSum
```

**可以用前缀和数组简化dp内部计算，但是前缀和的计算已经是O(N)了**