## Target Sum

### 带备忘录的回溯

```
class Solution:
    def findTargetSumWays(self, nums: List[int], target: int) -> int:

        def traverse(path, index):
            if index == n:
                if path == target:
                    return 1
                else:
                    return 0
            if memo.get((index, path)) != None:
                return memo[(index, path)]
            else:
                memo[(index, path)] = traverse(path + nums[index], index+1) + traverse(path - nums[index], index+1)
            return memo[(index, path)]
        memo = dict()
        n = len(nums)
        return traverse(0, 0)
```

### 动态规划
$$neg=\frac{sum−target}{2}$$

```
class Solution:
    def findTargetSumWays(self, nums: List[int], target: int) -> int:
        
        if abs(target + sum(nums)) % 2 != 0:
            return 0

        target = abs(target + sum(nums)) // 2
        dp = [0] * (target+1)
        dp[0] = 1
        for num in nums:
            for j in range(target, -1, -1):
                if j >= num:    
                    dp[j] = dp[j] + dp[j-num]
        return dp[target]

```