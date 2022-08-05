## Partition Equal Subset Sum

### 二维dp的背包问题

```
class Solution:
    def canPartition(self, nums: List[int]) -> bool:
        sums = sum(nums)
        n = len(nums)
        if sums % 2 != 0:
            return False
        sums = sums // 2
        dp = [[False] * (sums+1) for _ in range(n+1)] 
        
        for i in range(n+1):
            dp[i][0] = True
        for i in range(1, n+1):
            for j in range(1, sums+1):
                if j - nums[i-1] < 0:
                    dp[i][j] = dp[i-1][j]
                else:
                    dp[i][j] = dp[i-1][j-nums[i-1]] or dp[i-1][j]
        return dp[n][sums]
```

### 空间使用降维1D的情况

**为什么j是反向遍历的？**  
1.先看原来2D情况，dp[i][j]的值，都是仅依靠上一行dp[i-1][...]得出的。意思是我们要算当前dp[i]行的值，仅需要上一行dp[i-1]就好。所以可以将其转化为：原地更新1D数组问题；

2.现在考虑降为1D，定义该1D数组为int[] dp。回忆原来2D情况，dp[i][j]的值都是依靠“其正上方的值dp[i-1][j]+左上方的值dp[i-1][j-nums[i]]”来更新。那么如果对1D进行正向遍历即从dp[0]->dp[n-1]填充，对于某一位例如dp[cur]的更新，势必会用到dp[pre]（pre<cur），因为是正向遍历，那么dp[pre]在当前轮次已经被更新过了，当在这种情况下计算的dp[cur]肯定不正确（其实说白了，就相当于2D情况下，使用了同一行的值。例如使用dp[i][j-nums[i]]来更新dp[i][j]）；

3.现在解释对1D数组进行反向遍历即从dp[n-1]->dp[0]填充。同样，对于某一位例如dp[cur]的更新，势必会用到dp[pre]（pre<cur）。但注意，因为是从后往前进行遍历的，此时dp[pre]在当前轮次未被更新，所以就相当于2D情况下使用的上一行的值，这样计算就是正确的了。

```
class Solution:
    def canPartition(self, nums: List[int]) -> bool:
        sums = sum(nums)
        n = len(nums)
        if sums % 2 != 0:
            return False
        sums = sums // 2
        dp = [False] * (sums+1)
        dp[0] = True

        for i in range(1, n+1):
            for j in range(sums, -1, -1):
                if j - nums[i-1] >= 0:
                    dp[j] = dp[j] or dp[j-nums[i-1]]
                
        return dp[-1]
```

