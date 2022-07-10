## Subsets

```
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:

        def backtrack(subset: List[int], start: int):
            result.append(subset)

            for idx in range(start, size):
                backtrack(subset+[nums[idx]], idx+1)
        
        size = len(nums)
        result = []
        backtrack([], 0)
        return result
```