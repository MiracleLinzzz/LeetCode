## Minimum ASCII Delete Sum for Two Strings

### 递归

```
class Solution:
    def minimumDeleteSum(self, s1: str, s2: str) -> int:
        
        def dp(i, j):
            if i == m:
                res = 0
                for k in range(j, n):
                    res += ord(s2[k])
                return res
            if j == n:
                res = 0
                for k in range(i, m):
                    res += ord(s1[k])
                return res

            if memo[i][j] != -1:
                return memo[i][j]
            
            if s1[i] == s2[j]:
                memo[i][j] = dp(i+1, j+1)
            else:
                memo[i][j] = min(
                    ord(s1[i]) + dp(i+1, j),
                    ord(s2[j]) + dp(i, j+1) 
                )
            return memo[i][j]

        m = len(s1)
        n = len(s2)
        memo = [[-1 for _ in range(n)] for _ in range(m)]
        return dp(0, 0)
```

### 迭代

```
class Solution:
    def minimumDeleteSum(self, s1: str, s2: str) -> int:
        m = len(s1)
        n = len(s2)
        dp = [[0 for _ in range(n+1)] for _ in range(m+1)]
        for i in range(1, m+1):
            dp[i][0] = dp[i-1][0] + ord(s1[i-1]) 
        for j in range(1, n+1):
            dp[0][j] = dp[0][j-1] + ord(s2[j-1])
        
        for i in range(1, m+1):
            for j in range(1, n+1):
                if s1[i-1] == s2[j-1]:
                    dp[i][j] = dp[i-1][j-1]
                else:
                    dp[i][j] = min(
                        ord(s1[i-1]) + dp[i-1][j],
                        ord(s2[j-1]) + dp[i][j-1]
                    )
        return dp[m][n]
```

### 另一种递归，比较省时间

```
class Solution:
    def minimumDeleteSum(self, s1: str, s2: str) -> int:
        # 转化为最长公共子序列(lcs)问题，用总的ascii值减去相同的值即可
        m, n = len(s1), len(s2)
        dp = [[0] * (n+1) for _ in range(m+1)]
        # 分为两种情况，s1的第i个元素和s2的第j个元素相等和不相等
        for i, ch1 in enumerate(s1):
            for j, ch2 in enumerate(s2):
                if ch1 == ch2:
                    dp[i+1][j+1] = dp[i][j] + ord(ch1)
                else:
                    dp[i+1][j+1] = max(dp[i][j+1], dp[i+1][j])
        # 分别得到两个的ascii值
        ord1, ord2 = 0, 0
        for ch in s1:
            ord1 += ord(ch)
        for ch in s2:
            ord2 += ord(ch)
        return ord1 + ord2 - 2 * dp[-1][-1]
```