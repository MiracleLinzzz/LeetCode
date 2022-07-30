## Longest Increasing Subsequence

### 朴素的动态规划解法 O(N^2)
```
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        dp = [1 for _ in range(len(nums))]

        for i in range(1, len(nums)):
            for j in range(i+1):
                if nums[i] > nums[j]:
                    dp[i] = max(dp[i], dp[j]+1)
        return max(dp) 
```

### 纸牌游戏解法 二分查找

```
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        
        top = []
        files = 0

        for num in nums:
            left = 0
            right = files
            while left < right:
                mid = left + (right-left) // 2
                if top[mid] < num:
                    left = mid + 1
                else:
                    right = mid
            if left >= files:
                top.append(num)
                files += 1
            else:
                top[left] = num

        return files
```