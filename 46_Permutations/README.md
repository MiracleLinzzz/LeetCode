## Permutations

**注意是没有重复数字**
多一步判断重复数字
- 多一个bool数字
- 或者number in set()

```
class Solution:
    def permute(self, nums: List[int]) -> List[List[int]]:

        def backtrack(permutation: List[int]):

            if len(permutation) == n:
                permutations.append(permutation[:])
                return
            
            for idx in range(n):
                if nums[idx] in permutation:
                    continue
                else:
                    permutation.append(nums[idx])
                    backtrack(permutation)
                    permutation.pop()

        n = len(nums)
        permutations = []
        permutation = []
        backtrack(permutation)

        return permutations

        
```