## Edit Distance

### 递归的备忘录方法

```
class Solution:
    def minDistance(self, word1: str, word2: str) -> int:
        def dp(word1, s1, word2, s2):
            if s1 < 0:
                return s2 + 1
            if s2 < 0:
                return s1 + 1

            if memo[s1][s2] != -1:
                return memo[s1][s2]


            if word1[s1] == word2[s2]:
                memo[s1][s2] = dp(word1, s1-1, word2, s2-1)
            else:
                memo[s1][s2] = Min(
                    dp(word1, s1-1, word2, s2-1)+1,
                    dp(word1, s1, word2, s2-1)+1,
                    dp(word1, s1-1, word2, s2)+1
                ) 
            return memo[s1][s2]
            
        def Min(x, y, z):
            return min(x, min(y, z))

        m = len(word1)
        n = len(word2)
        memo = [[-1 for _ in range(n)] for _ in range(m)]

        return dp(word1, m-1, word2, n-1)
        
```

### 迭代的DP Table方法

```
class Solution:
    def minDistance(self, word1: str, word2: str) -> int:       
        def Min(x, y, z):
            return min(x, min(y, z))
        m = len(word1)
        n = len(word2)
        dp = [[-1 for _ in range(n+1)] for _ in range(m+1)]
        for i in range(m+1):
            dp[i][0] = i
        for j in range(n+1):
            dp[0][j] = j
        
        for i in range(1, m+1):
            for j in range(1, n+1):
                if word1[i-1] == word2[j-1]:
                    dp[i][j] = dp[i-1][j-1]
                else:
                    dp[i][j] = Min(dp[i-1][j-1]+1, dp[i][j-1]+1, dp[i-1][j]+1)
        return dp[m][n]
```