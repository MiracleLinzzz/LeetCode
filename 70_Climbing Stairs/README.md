## Climbing Stairs

```
class Solution:
    def climbStairs(self, n: int) -> int:
        if n == 1 or n == 2:
            return n

        dp_0 = 1 
        dp_1 = 1
        for j in range(2, n+1):
            dp = dp_1 + dp_0
            dp_0 = dp_1
            dp_1 = dp 
        return dp
```

```
class Solution:
    def climbStairs(self, n: int) -> int:
        coins = [1, 2]
        m = 2
        dp = [0] * (n+1)
        dp[0] = 1 

        for j in range(1, n+1):
            for coin in coins:
                if j - coin >= 0:
                    dp[j] = dp[j] + dp[j-coin]
        return dp[-1]
```