## Last Stone Weight II

```
class Solution:
    def lastStoneWeightII(self, stones: List[int]) -> int:
        target = sum(stones) // 2
        dp = [0] * (target+1)
        dp[0] = 0

        for stone in stones:
            for i in range(target, -1, -1):
                if i >= stone:
                    dp[i] = max(dp[i], stone + dp[i-stone])

        return sum(stones) - 2*dp[-1]


```