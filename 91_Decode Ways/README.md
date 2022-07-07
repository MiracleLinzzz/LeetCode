## Decode Ways

```
class Solution:
    def numDecodings(self, s: str) -> int:
        if s[0] == "0":
            return 0
        n = len(s) 
        dp = [1] * n
        for idx in range(1, n):
            if s[idx] == "0":
                if "1" <= s[idx-1] + s[idx] <= "26":
                    dp[idx] = dp[idx-2]
                else:
                    return 0
            else:
                if "1" <= s[idx-1] + s[idx] <= "26":
                    dp[idx] = dp[idx-1] + dp[idx-2]
                else:
                    dp[idx] = dp[idx-1]
        return dp[-1]

```