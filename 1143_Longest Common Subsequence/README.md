## Longest Common Subsequence

### 递归

```
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        def dp(s1, s2):
            if s1 < 0 or s2 < 0:
                return 0
            
            if memo[s1][s2] != -1:
                return memo[s1][s2]

            if text1[s1] == text2[s2]:
                memo[s1][s2] = 1 + dp(s1-1, s2-1)
            else:
                memo[s1][s2] = max(
                    dp(s1-1, s2),
                    dp(s1, s2-1)
                )
            return memo[s1][s2]

        m = len(text1)
        n = len(text2)
        memo = [[-1 for _ in range(n)] for _ in range(m)]
        return dp(m-1, n-1)

```

### 迭代

```
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        m = len(text1)
        n = len(text2)
        dp = [[0 for _ in range(n+1)] for _ in range(m+1)]
        
        for i in range(1, m+1):
            for j in range(1, n+1):
                if text1[i-1] == text2[j-1]:
                    dp[i][j] = 1 + dp[i-1][j-1]
                else:
                    dp[i][j] = max(
                        dp[i][j-1],
                        dp[i-1][j]
                    )
        return dp[m][n]
```