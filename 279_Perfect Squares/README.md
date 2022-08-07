## Perfect Squares

### 动态规划

```
class Solution:
    def numSquares(self, n: int) -> int:
        coins = []
        for i in range(1, int(sqrt(n))+1):
            coins.append(i**2)

        dp = [n] * (n+1)
        dp[0] = 0

        for coin in coins:
            for j in range(1, n+1):
                if j >= coin:
                    dp[j] = min(dp[j-coin] + 1, dp[j])

                    
            
        return dp[-1]
```

### 贪心算法

```
class Solution:
    def numSquares(self, n: int) -> int:
        coins = []
        for i in range(1, int(sqrt(n))+1):
            coins.append(i**2)

        def divisible(remain, count):
            if count == 1: return remain in coins
            for coin in coins:
                if divisible(remain-coin, count-1):
                    return True
            return False
        
        for count in range(1, n+1):
            if divisible(n, count):
                return count

```