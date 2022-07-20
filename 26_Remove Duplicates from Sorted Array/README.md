## Remove Duplicates from Sorted Array

快慢指针

```
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        fast = 0
        slow = 0
        while fast < len(nums):
            if nums[fast] != nums[slow]:
                slow += 1
                if fast > slow:
                    nums[slow] = nums[fast]
            fast += 1
        
        return slow + 1
```

所谓通用解法 其实也是双指针的一种变式  
从可以重复一个 变成了k个

```
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        idx = 0
        for x in nums:
            if idx < 1 or nums[idx-1] != x:
                nums[idx] = x
                idx += 1
        return idx
```