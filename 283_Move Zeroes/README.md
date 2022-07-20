## Move Zeroes

结合27题 《移除元素》 的做法的拓展结果

```
class Solution:
    def moveZeroes(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        slow = 0
        fast = 0
        while fast < len(nums):
            if nums[fast] != 0:
                nums[slow] = nums[fast]
                slow += 1
            fast += 1
        for p in range(slow, len(nums)):
            nums[p] = 0
```


交换数字的思路

```
class Solution:
    def moveZeroes(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        slow = 0
        fast = 0
        while fast < len(nums):
            if nums[fast] != 0:
                temp = nums[fast]
                nums[fast] = nums[slow]
                nums[slow] = temp
            if nums[slow] != 0:
                slow += 1
            fast += 1
```