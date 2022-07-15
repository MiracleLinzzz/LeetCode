## Sort an Array

这一题有几个小tips
1. 取的范围都是左闭右闭 -- 左闭右开我一直没有特别好的写法
2. 事先设置一个temp变量储存交换时的变量，避免了在递归中频繁分配和释放内存可能产生的性能问题。
3. merge用的是双指针技巧进行的排序，不是in-place？
4. 所以从整体上看，这个二叉树的高度是 logN，其中每一层的元素个数就是原数组的长度 N，所以总的时间复杂度就是 O(NlogN)。

```
class Solution:
    def sortArray(self, nums: List[int]) -> List[int]:
        self.temp = [0 for _ in range(len(nums))]
        self.sort(nums, 0, len(nums)-1)
        return nums

    
    def sort(self, nums: List[int], left: int, right: int):
        if left == right:
            return 

        mid = left + (right - left) // 2
        self.sort(nums, left, mid)
        self.sort(nums, mid+1, right)

        self.merge(nums, left, mid, right)

    def merge(self, nums: List[int], left: int, mid: int, right: int):
        for p in range(left, right+1):
            self.temp[p] = nums[p]
        i = left
        j = mid + 1
        for p in range(left, right+1):
            if i == mid + 1:
                nums[p] = self.temp[j]
                j += 1
            elif j == right + 1:
                nums[p] = self.temp[i]
                i += 1  
            elif self.temp[i] > self.temp[j]:
                nums[p] = self.temp[j]
                j += 1
            elif self.temp[i] <= self.temp[j]:
                nums[p] = self.temp[i]
                i += 1  


```