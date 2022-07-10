## Subsets II


### 使用used标记矩阵
```
class Solution:
    def subsetsWithDup(self, nums: List[int]) -> List[List[int]]:

        def backtrack(subset: List[int], start: int, used: List[int]):

            subsets.append(subset[:])

            
            for idx in range(start, size):
                if idx > 0 and nums[idx] == nums[idx-1] and used[idx-1] == 0:
                    continue
                used[idx] = 1
                subset.append(nums[idx])
                backtrack(subset, idx+1, used)
                subset.pop()
                used[idx] = 0

        subsets = []
        size = len(nums)
        used = [0 for _ in range(size)]
        nums.sort()
        backtrack([], 0, used)
        return subsets
```


### 不使用used标记矩阵
```
class Solution:
    def subsetsWithDup(self, nums: List[int]) -> List[List[int]]:

        def backtrack(subset: List[int], start: int):

            subsets.append(subset[:])

            
            for idx in range(start, size):
                if idx > start and nums[idx] == nums[idx-1]:
                    continue
                subset.append(nums[idx])
                backtrack(subset, idx+1)
                subset.pop()

        subsets = []
        size = len(nums)
        nums.sort()
        backtrack([], 0)
        return subsets
```